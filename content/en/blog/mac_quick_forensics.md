---
author: "Wren Howell"
title: "Mac Quick Forensics"
date: 2026-04-19
description: "Exploring Mac Artifacts"
tags: ["More Mac Artifacts"]
thumbnail: https://images.hindustantimes.com/tech/img/2024/11/18/1600x900/michail-sapiton-alCEnNmzhPE-unsplash_1690168039471_1731933823093.jpg
---

Recently, I had to write a playbook for Macs from a incident response perspective. Even though I had experience investigating Macs before, because I did not do it in such a long time, I struggled through the investigation more than I would have. So I decided to make a guide that will be helpful for me in the future.  This will expand on the previous blog post about Mac persistence mechanisms and provide additional forensic artifacts that a investigator could look at that could be of value. This blog will also link some amazing blog posts by some amazing Mac researchers.

### Looking at Launch Agents and Launch Daemons

**Description**

LaunchAgents and LaunchDaemons are the standard macOS mechanisms for starting programs automatically at user login or system boot. 

**Forensic significance**

Launch Agents and Launch Daemons are by far the most common place for persistence. Some important plist properties to look at are:

- RunAtLoad property is true: indicates execution at load time and a sign of persistence 
- StartInterval or StartCalendarInterval:  define scheduled execution
- KeepAlive: also an indication of persistence

```
users.homedir/Library/LaunchAgents/
/System/Library/LaunchAgents 
/System/Library/LaunchDaemons 
```

**Useful command**
```bash
plutil -p <file.plist>
```
Renders the plist in a readable format so you can quickly see what binary or script it is pointing to.

**If malicious LaunchAgent/LaunchDaemon is found**

```bash
launchctl unload /path/to/suspicious.plist
```

This will stop the running process and deregisters it. Remove the malicious plist. 

> **Tip:** Additional persistence mechanisms are documented at [loobins.io](https://www.loobins.io).


---

### Looking at shell commands and execution history like zshell

**Description**

Shell history record commands entered by the system. Since 2019, zshell has been the default shell for macOS. 

**Forensic significance**

Looking at shells can provide evidence to see what was run on the system.  


**Location for zshell**

```
/Users/usersname/.zsh_history
```

**What to look for**

Look for strange curl commands, attempts of installation of unfamiliar programs, unusual scripts running. 

---

### Looking at Browser History 

**Description**

Browser history shows the where the sites that the user navigated to. 

**Forensic significance**

 Looking at browser history is one of the quickest ways to find root cause of infection. It can help determine root cause like whether the user clicked on a phishing link, or went to a suspicious site that led to the initial infection. Different browser have their browser history artifact in varying locations. Common browser and their locations are listed below.

**Locations by browser**

| Browser | Path |
|---------|------|
| Safari | `~/Library/Safari/History.db` |
| Chrome | `~/Library/Application Support/Google/Chrome/History` |
| Firefox | `/Library/Application Support/Firefox/Profiles/*/` |

---

### Looking at User Downloads 

**Description**

User downloads shows files that a user downloads from the Internet. 

**Forensic significance**

Looking at downloads, is also a quick way to find potential malicious artifacts. 

**Locations**

```
/Users/usersname/Downloads
```

**Useful command**

```bash
xattr -l <file>
```
Lists all extended attributes on a file, including the quarantine URL showing where the download originated.

---

### Looking at Unified Audit Logs

**Description**

Unified logging is a centralized logging system for macOS. The system collects logs from the kernel, OS processes, and third-party apps into a single binary store. Entries are stored in .tracev3 files and best viewed through the terminal.


**Forensic significance**

It shows things like process execution, network activity, and much more. It is a very verbose log source that can be vital in forensic investigations. 


**Locations**

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




<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
</style>

