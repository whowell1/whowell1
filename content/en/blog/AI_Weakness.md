---
author: "Wren Howell"
title: "Addressing LLM Limitations "
date: 2025-04-12
description: "Weakness in LLMs"
tags: ["Prompt Injection, Hallucinations"]
thumbnail: https://eu-images.contentstack.com/v3/assets/blt6d90778a997de1cd/blt621ce6e29b55c494/670d41be3dbe55de0cb9db4b/LLM(1800)_Krot_Studio_Alamy.jpg?width=1280&auto=webp&quality=95&format=jpg&disable=upscale
---

The AI hype has finally gotten to me too.

I have avoided writing about AI for a while because the space moves too quickly. Anything you publish risks becoming obsolete within days. Recently, though, my LinkedIn feed has been saturated with discussion of Model Context Protocol. Engineers are testing it in real time while the hype cycle treats it as the next breakthrough. At the same time, Google announced its own agent protocol, A2A. Engineers will experiment with it and sales teams will inevitably amplify it.

Despite progress in large language models, two fundamental problems remain unsolved. Prompt injection and hallucinations.

**Prompt Injection**

A prompt injection attack occurs when an attacker manipulates model input so the LLM produces unintended or unsafe behavior. This can happen directly through malicious user input or indirectly through compromised third party data that gets passed into the model.

The root issue is architectural. LLMs are designed to trust their inputs. They do not distinguish between instructions and data. As models gain access to tools, APIs, filesystems, and automation workflows, the blast radius grows. More integrations mean more opportunities to smuggle instructions through untrusted content.

In short, this is not just a bug. It is a core feature of how these systems work.

**Update (https://simonwillison.net/2025/Apr/11/camel/) April 13th via blog by Sam Wilson** 

Sam Wilson proposed a way to combat prompt injection. The mitigation strategy introduces two separate models. A privileged LLM handles only trusted inputs and is allowed to take actions. A quarantined LLM processes untrusted data such as emails or documents but is sandboxed and restricted to extraction tasks.

The design also adds explicit control flow so users can see and approve what the system intends to execute, similar to reviewing a script before it runs.

This layered approach improves isolation and transparency. However, it introduces a question of practicality. If users must approve every step, they may eventually stop reviewing and simply click yes (like what happens during MFA fatigue). At that point, the safety control becomes theater rather than protection. 

**LLM Hallucinations**

Hallucinations occur when an LLM generates information that is incorrect or entirely fabricated. These systems do not know facts because they work by  predicting tokens based on statistical patterns. A useful mental model on how an LLM works would be an sophisticated autocomplete trained on on the internet. These models have gotten better, but they are not all-knowing or can reason like human beings. 

With new protocols emerging and tooling becoming more complex, it is worth slowing down and examining the tradeoffs. These systems are powerful but not trustworthy by default. As defenders and engineers, we need to design around their shortcomings and understand the weaknesses in their system to know how we can best use them.


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
