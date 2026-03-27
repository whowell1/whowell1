---
author: "Wren Howell"
title: "The Importance of using Cyber Deception as Part of Cybersecurity Strategy"
date: 2025-03-10
description: "Using Cyber Deception"
tags: ["Cyber Deception, Decoys, Honeytoken"]
thumbnail: https://upload.wikimedia.org/wikipedia/commons/3/32/Matsumoto_castle_3.jpg
---

AI and LLMs have changed cybersecurity, but the real shift isn't AI-generated malware. It's how attackers operate.

Attackers are having an easier time compromising systems by using stolen credentials, abusing legitimate tools through living off the land and living off the orchard techniques, and compromising supply chains that enable them to persist in an environment for a long time before taking action.

At the same time, security teams are dealing with tighter budgets, smaller teams, and higher expectations. Even organizations with decent funding struggle to maintain visibility when attackers are this good at staying hidden.

You can't just work harder. You need a different approach.

That's where cyber deception becomes an important part of your cybersecurity strategy. By incorporating deception, organizations can shift the advantage back in their favor and create uncertainty for attackers. 

## What is the Current Strategy?

### Analogy: Protect the King in the Castle

The current defense strategy is pretty straightforward: **protect the king in the castle and equip the castle with the best guns.**

This works if you assume your infrastructure won't change much. But anyone who's worked in IT knows that's not realistic. You're constantly upgrading tools, training staff, dealing with projects that take longer than expected, and adjusting to new requirements.

The bigger problem though is when you focus all your defenses around specific assets, you're basically telling attackers where the valuable stuff is. They know what to look for, they know where your critical systems probably are, and they know what security tools you're likely running. The approach is predictable.

## What is Cyber Deception?

### Analogy: Build Many Castles

Deception takes a different approach: **You build multiple castles that all look equally defended. Only you know where the king actually is**

When an attacker gets into your environment:
- The noise they generate touching decoys becomes your alert; they reveal themselves by interacting with things they shouldn't
- You collect intelligence on what they're doing and what techniques they're using
- You gain time to strengthen defenses where you need them
- You can address gaps in your security before real damage happens

The attacker has to guess which castle holds the king, burning time and resources while you watch, learn, and respond.

## Why This Works Well with EDR

### Combining Deception with EDR

EDR tools are good at detecting known threats and suspicious behavior on endpoints. But they work better when they have context about what's happening across your environment.

Deception can enhance EDR in a few ways:

**Early Warning**
Deception can catch attackers during reconnaissance, before they reach real assets. This gives security teams a chance to hunt proactively instead of reacting to an alert after damage is done.

**High-Fidelity Alerts**
Deception generates fewer false positives; there's no legitimate reason for anyone to touch a decoy. This reduces alert fatigue, which is a real problem when your team is drowning in alerts from other tools.

**Attacker Intelligence**
You can observe attacker techniques in real-time and feed that intelligence into your detection rules. This makes your other tools smarter.

**Extended Visibility**
Deception fills visibility gaps where EDR agents might not be deployed; legacy systems, network segments without coverage, systems that can't run modern EDR. It creates tripwires across your environment.

**Slows Down Attackers**
When attackers interact with decoys, it gives your incident response team time to contain the threat before exfiltration happens. It also forces attackers to be noisier, which makes EDR detection easier.

### How This Works Together

When an attacker touches a decoy:
1. The deception system alerts immediately; this is a high-confidence threat
2. EDR investigates the source endpoint for compromise indicators
3. Your security team analyzes attacker TTPs from deception logs
4. EDR hunts proactively for similar behavior across all endpoints
5. Your response team contains the threat before it reaches critical assets

This creates defense-in-depth where deception provides early detection and EDR provides detailed endpoint visibility and response capabilities.

## Getting Deception Running in Your Environment

### 1. Identify the Crown Jewels

You can't protect what you don't know about.

Start by mapping your critical assets; databases, file servers, domain controllers, sensitive applications. Figure out where your most valuable data lives, what paths attackers would take to reach it, and which systems would cause the most damage if compromised.

This matters because deception works best when it's deployed strategically around your actual crown jewels. You need to know what you're protecting before you can create convincing distractions around it.

### 2. Create Believable Decoys

Your decoys need to look real. If they look fake or abandoned, sophisticated attackers will ignore them.

Deploy fake servers, workstations, and databases that match your actual infrastructure. Plant fake credentials in files, memory, and configuration files. Create decoy network shares with realistic-looking documents. Make sure decoys have appropriate names, roles, and purposes that fit your environment.

The goal is making them indistinguishable from real assets.

### 3. Set Up Alerts and Triage

Make sure your team knows when a decoy has been touched.

Integrate deception alerts with your SIEM and EDR. Create clear escalation procedures for deception events. Train your security team to recognize and respond to these alerts. Establish playbooks for investigating deception triggers.

A deception alert is one of the highest-fidelity signals you can get; there's no legitimate reason for anyone to interact with a decoy. But this only works if your team knows how to act on these alerts quickly.

### 4. Test from an Attacker's Perspective

After deploying decoys, approach them like an attacker would. If you brought in a red teamer to find the decoys, would they spot them? What non-technical controls could make the decoys more convincing and harder to distinguish from real assets?

**Why this matters:** Decoys only work if they're believable. Regular testing from an adversarial perspective helps ensure your decoys stay effective as your environment and attacker techniques evolve.

## Getting Started

**Start Small:**
1. Deploy a few decoy credentials in common locations; I've written about doing this with SharePoint decoys before
2. Create 2-3 fake servers that look important
3. Monitor for any interactions
4. Use findings to improve your real defenses

**Scale Gradually:**
- Add more decoys as you learn what works
- Expand coverage to different network segments
- Integrate more deeply with EDR and SIEM
- Refine based on attacker behavior you observe

**Measure Success:**
- Time to detect threats (should decrease)
- Quality of threat intelligence gathered
- Number of attacks caught before reaching real assets
- Reduction in dwell time for threats

## Conclusion

The cybersecurity landscape has changed. Attackers are smarter and more evasive. Traditional defense strategies are necessary but not sufficient anymore.

Deception shifts you from purely reactive to proactive. You create uncertainty for attackers, get early warning of threats, and gather intelligence that makes your other security tools more effective.

Don't just build a better castle. Build multiple castles and let attackers waste their time revealing themselves while your real assets stay hidden and protected.

{{< css.inline >}}

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
{{ $image := $resource.Fit "600x400" }}
</style>

{{< /css.inline >}}
