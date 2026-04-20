---
author: "Wren Howell"
title: "Looking at More Mac Forensic Artifacts"
date: 2026-04-19
description: "Exploring Mac Artifacts"
tags: ["More Mac Artifacts"]
thumbnail: https://images.hindustantimes.com/tech/img/2024/11/18/1600x900/michail-sapiton-alCEnNmzhPE-unsplash_1690168039471_1731933823093.jpg
---

Recently, I had to write a playbook for Macs from a incident response perspective. Even though I had experience investigating Macs before, because I did not do it in such a long time, I struggled through the investigation more than I would have. So I decided to make a guide that will be helpful for me in the future.  This will expand on the previous blog post about Mac persistence mechanisms and provide additional forensic artifacts that a investigator could look at that could be of value. This blog will also link some amazing blog posts by some amazing Mac researchers.

## Launch Agents and Launch Daemons

LaunchAgents and LaunchDaemons are the standard macOS mechanisms for starting programs automatically at user login or system boot. These are by far the most common place for persistence. Some important plist properties to look at are:

- RunAtLoad property is true: indicates execution at load time and a sign of persistence 
- StartInterval or StartCalendarInterval:  define scheduled execution
- KeepAlive: also an indication of persistence

### Location of Launch Agent and Launch Daemons

```
users.homedir/Library/LaunchAgents/
/System/Library/LaunchAgents 
/System/Library/LaunchDaemons 
```

**Potentially Useful Commands**

To render the plist in a readable format run

```bash
plutil -p <file.plist>
```

If malicious LaunchAgent/LaunchDaemon is found. Run the command below to stop the plist and deregister it

```bash
launchctl unload /path/to/suspicious.plist
```

Then run the next command to remove the plist. 

```bash
rm /path/to/suspicious.plist
```

> **Tip:** Additional living off the orchard mechanisms are documented at [loobins.io](https://www.loobins.io).

--- 

## Shell History

Since macOS Catalina (2019), Zsh has been the default shell. Shell history files records commands entered by the user and can provide direct evidence of what was executed on the system.

### Location of zsh 

```
/Users/usersname/.zsh_history
```

*** What to look for ***

- Unusual curl or wget commands
- Installation of unfamiliar programs
- Obfuscated or encoded scripts being executed

--- 

## Browser History 

Browser history shows the sites the user navigated to. It is one of the quickest ways to establish root cause of an infection. 

Locations by browser

| Browser | Path |
|---------|------|
| Safari | `~/Library/Safari/History.db` |
| Chrome | `~/Library/Application Support/Google/Chrome/History` |
| Firefox | `/Library/Application Support/Firefox/Profiles/*/` |

--- 

## User Downloads 

The Downloads folder contains files retrieved from the internet and is a quick place to look for potentially malicious artifacts.

### Location

```
/Users/usersname/Downloads
```

**Potentially Useful Command**

```bash
xattr -l <file>
```
Lists all extended attributes on a file, including the quarantine URL showing where the download originated.

--- 

## Unified Audit Logs

Unified logging is a centralized logging system for macOS. The system collects logs from the kernel, OS processes, and third-party apps into a single binary store. Entries are stored in .tracev3 files and best viewed through the terminal or Console.app. It shows things like process execution, network activity, and much more. It is a very verbose log source that can be vital in forensic investigations. 


### Location of Unified Audit Logs

```
/var/db/diagnostics/
/var/db/uuidtext/
```

---

References

- https://www.elastic.co/guide/en/security/8.19/persistence-via-suspicious-launch-agent-or-launch-daemon.html 
- https://github.com/nlscott/macOS-Security
- https://oliviagallucci.com/blog/
- https://www.loobins.io