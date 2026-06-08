---
author: "Wren Howell"
title: "Part I: Exploring the Technical Infrastucture of LLM and its Impact of Security Practioners"
date: 2026-04-10
description: "Understanding the technical language of LLMs and its relationship to security work"
tags: ["LLMs, AI, Security AI"]
thumbnail: https://blog.adobe.com/security/media_11634bb135281c9b51d236031f2c0d6c7d92336b3.jpg?width=750&format=jpg&optimize=medium
---


Artificial intelligence (AI) is the new buzzword businesses use to capture the attention of customers, employees, and the board. There are many "experts" in AI who claim it will take over the world. With so many hyperbolic takes, I wanted to take a step back and winnow out the hype from reality. 

The initial idea for this blog post came from Luke Kanies, who wrote about how AI was impacting mobile developers. At first, I wanted to write something similar for security professionals, because aside from Marcus Hutchins, there were few honest blog posts geared toward a general audience on how AI was affecting the security community. However, as I started writing, the noise around the grand promises of AI became louder, which frustrated me. I realized that my initial points were incomplete. This frustration led me on a deeper intellectual journey to understand AI: what it is, the technical, financial, and cognitive infrastructure behind it, and what we risk losing as humans if we start to depend on it. This blog, in whatever published form it takes, draws inspiration from many writers, researchers, journalists, and others. The links to their works are cited in the post's references.

Understanding the Technical Infrastructure

Understanding the Technical Jargon
One of the very first things I noticed when engaging with others about the impact of AI on society was that they did not have a good grasp of the different job descriptions and the technical concepts I take for granted in the tech field.

Software Developers

Software developers write the code that powers the applications people use today. Building software is like building a facility for a family that is always growing. As requirements change, the facility will need to be updated to accommodate the growing number of people. Sometimes the facility needs small additions; sometimes, it needs major architectural changes while still keeping the various parts of the house intact. Just as this builder does, software developers navigate changes in business, technology, and customer needs while ensuring the product is working and secure. Just as a builder needs to work with people with diverse skill sets (plumbers, electricians, carpenters, roofers, etc.) to help build a facility, software developers have diverse skill sets and work with various teams to build software. Some of these skills and specialties in software engineering are listed below.

- Front-End Developer: builds everything a user sees and interacts with.
- Back-End Developer: builds the behind-the-scenes infrastructure and business logic.
- Full-Stack Developer: does both back-end and front-end work.
- Mobile Developer: builds applications for iPhone and Android.
- Dev-ops Developer: builds pipelines and helps ship code from the laptop to production.

Information Technology (IT) Security/Security practitioners 

IT security professionals protect systems, networks, and data from unauthorized access, damage, or attack. Even though software developers can be IT security professionals, and IT security professionals can be software developers, for most organizations, having the same team perform both tasks is too much to ask. For example, an organization that manages critical IT infrastructure, such as banking or power grids, requires many IT security professionals to monitor, update, and surveil nation-states that can have significant impacts on people. Some of these IT security skills and specialties are listed below in a simplified  way.

- Incident Response Analysts: Responds to active security breaches and cyberattacks, investigating what happened, containing the damage, and restoring systems to normal.
- Red Team: Simulate real-world attacks on an organization's systems to find vulnerabilities before actual attackers do.
- Detection Team: Monitor networks and systems for suspicious activity, building and tuning alerts to catch threats early.
- GRC Team: Ensure the organization adheres to security laws, regulations, and internal policies, manages risk, and maintains compliance documentation.

Artificial Intelligence (AI)

AI is a broad term that encompasses fields of computer and data science focused on building machines with human-like intelligence to perform tasks such as learning, reasoning, problem-solving, perception, and language understanding (https://www.mtu.edu/computing/ai/). AI as a domain has been around since the 1950s.  AI is used in commercial software for tasks such as recommendation engines and phishing email detection. What introduced AI into the cultural zeitgeist was the release of ChatGPT, a conversational chatbot built on a large language model (LLM).

Large Language Model (LLM)

Dr. Timnit Gebru, an AI researcher, describes language models as "systems trained on string prediction tasks, predicting the likelihood of a token (character, word, or string) given either its preceding context or (in bidirectional and masked LMs) its surrounding context" (https://s10251.pcdn.co/pdf/2021-bender-parrots.pdf). 

Artificial General Intelligence (AGI)

AGI is a type of artificial intelligence that matches or surpasses human capabilities across virtually all cognitive tasks (https://www.ibm.com/think/topics/artificial-general-intelligence).

These definitions are important because the tech industry often uses the terms AGI, LLM, and AI interchangeably, which can confuse the general public. The definition of AGI has not changed from a scientific perspective. However, despite clear definitions set by experts, tech CEOs and tech companies obscure and redefine these terms to suit their needs. The quotes by Sam Alman in 2025, 'AI systems can rival a legitimate PhD-level expert in any field,' and Dario Amadi's 2026 remark, 'I do not know if AI models are conscious,' are obvious examples of highly public figures conflating terms and confusing the public.

Explaining the Technical Tidbits of LLMs (Training, Benchmarking, RAG, and Inference)

Stage 1: Pre-training

The model starts by consuming a massive amount of text (trillions of words) from the Internet, including books, articles, code, and websites. It improves itself by repeatedly trying to predict the next word in a sentence, adjusting itself each time it gets it wrong, a process known as backpropagation. Over billions of examples, the model gradually develops a broad base of language, facts, and reasoning. This stage is by far the most resource-intensive, requiring thousands of GPUs to run for weeks or even months and costing tens to hundreds of millions of dollars.

Stage 2: Fine-tuning

Once pre-training is complete, the model is then specialized using smaller, carefully curated datasets. This fine-tuning step is where the model learns to follow instructions, answer questions in a structured way, and adapt to specific domains such as cybersecurity, medicine, or law. Think of it as taking someone with a broad general education and giving them focused, on-the-job training.

Stage 3: Alignment

The final stage is about shaping the model's behavior to ensure it is helpful, accurate, and safe. This is done through Reinforcement Learning from Human Feedback (RLHF), where human raters review and rank the model's responses. The model learns to favor highly rated responses, reducing harmful outputs and improving how well it follows instructions in ways users actually expect.

LLM Benchmarking

Benchmarking is a standardized framework for measuring and evaluating an LLM's performance (https://blog-datalab.com/making-sense-of-ai-benchmarks/). Huggingface, a popular open-source benchmark tool for LLMs, describes it as "a community-driven exam for AI." Benchmarking established a way to measure LLM progress that could be observed and verified by others.

Retrieval-Augmented Generation (RAG)

Marcus Hutchins, a security researcher, best describes RAG. He describes RAG as the ability for LLMs "to search the Internet for fresh data relevant to the user's query that allows it to use its training data to summarize information. This feature combines LLMs and search engines into a single product" (https://malwaretech.com/2025/08/every-reason-why-i-hate-ai.html). According to Microsoft (https://www.microsoft.com/en-us/microsoft-cloud/blog/2025/02/13/5-key-features-and-benefits-of-retrieval-augmented-generation-rag/), RAG helps LLMS retrieve current, up-to-date knowledge, provide contextual relevance, reduce hallucinations, reduce costs, and increase user productivity.

Inference

Inference is when an LLM produces predictions or conclusions, or, put more simply, the results of its output. When a user puts a prompt into a frontier model (OpenAI, ClaudeCode, xAI), the prompt is split into tokens and converted to numbers for matrix multiplication. This step, called prefill, is performed in parallel, enabling all input tokens to be processed simultaneously. "The decode step is where the model produces its output. It is an iterative process where the model generates one token at a time, with each new token being predicted based on the probability of all the tokens that came before it, until the full response is complete.

Technical Limitations of LLM's

Benchmark Limitations

The paper from James Fodor titled "Line Goes Up? Inherent Limitations of Benchmarks for Evaluating Large Language Models" outlines the limitations of benchmarks perfectly. He writes, "benchmarks suffer from overfitting, lack real-world relevance, and aren't validated against general cognitive performance." He continues to write that "LLMs consistently fail to learn the underlying structure of the tasks they are trained on, instead relying on complex statistical associations and heuristics which enable good performance on test benchmarks but generalize poorly to many real-world tasks." In simple terms, benchmarks are gamed to feign improvement, and they are, in themselves, a terrible way to measure LLM improvements.

Prompt Injection

Prompt injection occurs when users craft prompts that bypass or override the built-in safeguards. Even though there are ways to reduce  the likelihood of prompt injection, there is currently no way to prevent it completely.(https://genai.owasp.org/llmrisk/llm01-prompt-injection/).

LLM Hallucinations

Hallucinations are plausible but false statements generated by language models. According to OpenAI's own research, LLMs hallucinate "because standard training and evaluation procedures reward guessing over acknowledging uncertainty" (https://openai.com/index/why-language-models-hallucinate/). Just like prompt injection, hallucinations are a feature of LLMs, not a bug.

RAG Limitations

One way companies tried to address factual inaccuracies was through RAG. It turns out that searching the Internet for unverified sources and summarizing ideas did not lead to more accurate facts. RAG does not have a way to differentiate between a troll on Reddit or X and an expert when querying data, and it loses important context when retrieving data from the Internet.

Model Drift

Model drift is the degradation of a model's performance due to changes in the data it was originally trained on. Model drift happens because changes in the real world (language, facts, user behavior) shift the underlying patterns and relationships the model learned during training, making its predictions or outputs less accurate, relevant, or reliable over time.

Additional Risks To Consider When LLMs are Embedded in Our Applications

The promise of LLMs has led to a vibecoding, where developers use LLMs to generate functional code by simply describing what they need in plain language. The rise of vibe coding has tricked non-technical users into believing that they can code an app with just an idea and an LLM. Seasoned engineers are pushed to vibecode, too, as companies encourage them to use LLMs. Microsoft's CEO recently bragged that 30% of its code was vibecoded. Vibecoded apps introduce additional risks that even seasoned developers can overlook, which increase the attack surface.

Use of LLMs increases the Potential for Supply Chain Compromise

Building software is like building a car; different parts need to be shipped from different places to complete it. If the supplier that makes the engine is defective, then the integrity of the entire car is at risk. Similarly, in software, if the package used by the program is compromised, the entire program is at risk. The potential for software supply chain compromises increases when vibecoding because LLMs could hallucinate a malicious package that mimics a legitimate one and compromise the whole application. Historically, software supply chain packages have been a nightmare to detect, contain, and mitigate because of how dependent libraries are on each other. (e.g., Sha-hulud).  

Use of LLMs increases the Potential for Data Exfiltration

Data Exfiltration is the unauthorized transfer of data from a system or network to an external destination controlled by an attacker. The attack surface for data exfiltration expands significantly with LLM usage, as these systems are designed to accept broad inputs, making it difficult to prevent users from submitting sensitive information. Even with technical tools to minimize risk, a significant gap persists due to the fundamental design of LLMs. In highly regulated environments like healthcare or critical infrastructure, submitting sensitive information externally carries significant legal, operational, and reputational consequences, something most businesses cannot ignore.

Use of LLMs increases Fundamental Design Flaws

Since LLMs use publicly accessible internet data, they can build flawed systems that rely on insecure defaults. For example, when configuring a virtual machine in Microsoft Azure, an LLM will most likely leave all ports open to the Internet, mirroring the common but inherently insecure default configuration when building Azure VMs. Just as building a house without locks increases the risk of being robbed, building a VM with all ports open to the Internet leaves a company extremely vulnerable to breaches, something no organization would want.

How Improper Use of LLMs in Security Affects Security Operations

In the areas of security operations and cyber defense, LLMs' weaknesses are glaring. In this space, I see many LinkedIn posts claiming that AI-operated Security Operations Centers (SOCs) are a panacea for SOC problems. An AI SOC promises to fight alert fatigue, make analysts more skilled, and automate some tedious processes. As promising as this might sound, an "AI SOC" will be difficult to execute well. An AI-SOC will be difficult to implement effectively because the inherent limitations in LLMS compromise the CIA triad of security (confidentiality, integrity, and availability) in unpredictable ways that are crucial during security investigations. 
The first principle, confidentiality, ensures that information is accessible only to authorized parties, keeping data protected from unauthorized access or exposure. The second, integrity, ensures that data remains accurate and trustworthy, free from tampering or unauthorized alteration. The third, availability, ensures that data, systems, and services remain operational and accessible whenever authorized users need them.

During a security investigation, an LLM introduces risks across all three pillars of the CIA triad. Confidentiality is at risk because an LLM's inability to determine which information is confidential or sensitive, combined with its tendency to trust user input. During an investigation, analysts examine a variety of logs that contain sensitive information, including PII, system logs, and forensic artifacts. When this data is entered into an LLM unintentionally, the analyst has no control over where it goes. Microsoft has already acknowledged past instances of confidential data leaked to outside actors (https://www.bbc.com/news/articles/c8jxevd8mdyo). The cruel irony is that a tool deployed to assist in a security investigation can inadvertently prolong it. When an LLM leaks sensitive data, the organization has to manage two incidents simultaneously: the original breach and the one caused by the LLM itself, diverting resources and has the potential to extend  the investigation.

The integrity is at risk by the aforementioned tendency of LLMs to hallucinate, which includes reaching plausible but factually incorrect conclusions, misattributing indicators of compromise, or confidently recommending the wrong remediation steps. The tendency for LLMs to hallucinate is troubling in security operations where analysts are under significant pressure to find relevant logs to remediate the incident, leaving them vulnerable to cognitive shortcuts and to trusting hallucinated findings. Hallucinated findings can derail the entire investigation, causing analysts to chase non-existent threats and incorrect logs, while the threat actor continues to operate undetected. Acting upon hallucinated outputs can lead to destroying forensic evidence crucial to understanding the investigation, closing off recovery paths, or even destabilizing systems, prolonging and complicating incidents further.

The last part of the CIA triad, availability, is a risk as well. LLMs have a limited context window, which is the maximum amount of text they can process in a single interaction. The majority of security incidents require analysts to review large volumes of data from system logs, memory dumps, and tool logs, which are analyzed together to understand what happened. No current LLM has a sufficiently large context window to perform this analysis. Even though analysts could mitigate this limitation by feeding the LLM fragments of data, it introduces new problems. Critical information is omitted, increasing the likelihood that the LLM will draw incomplete or hallucinated conclusions. In addition, it introduces context rot, the tendency of LLMs to become less accurate and lose track of earlier information as a conversation grows longer. 

The Use of LLMs in Security

What I personally use LLMs for is very limited tasks like coming up with Kusto Query Language/Kibana Query Language (KQL) to help me write queries, rewrite regex filters, help rewrite emails, reformat things, rewrite some Dockerfiles, resolve syntax errors in my code, get started on reverse engineering basic obfuscation along with CyberChef, and aid in research and pulling data sources together. In addition, I spend part of my day experimenting with ways to bypass the guardrails built into these systems. For more complex tasks, LLMs' usefulness is limited, so I avoid them unless I can break them down into smaller tasks.   

As a security practitioner, the inherent limitations of LLMs make it almost impossible for me to trust their judgment in complex incident response cases. The potential ceiling for its use in security and coding seemed clear in a sandboxed environment, but the realities of the real world made its limitations clear, and the potential for catastrophic misuse, outweigh its benefits. However, the use of LLMs in security is not completely useless; they can find software vulnerabilities (but not because LLMs are good at finding vulnerabilities, we have toolings doing that for 10+ years), and be useful for creating creative honeypots that mimic real-world assets. Overall, the introduction of LLMs added more work to my colleagues. It has led to more people outsourcing their thinking to mathematical prediction machines that introduced more bugs because senior management measures productivity in lines of code written. In addition, it has led to the degradation of the services that we use every day, causing notable outages of tools and bloating software, examples of what Cory Doctrow calls "enshitification." My experience is starkly at odds with the salespeople of AI (product/project managers, former crypto bros, and C-suite executives) who claim that AI will somehow eliminate white-collar jobs, make software better, and make life easier. The irony is that if we continue to push these LLM's into our products aggressively, the inception of enshitification will continue, and it will be the security practitioners on the ground to tell the real story.


References 

- Gary Marcus (https://garymarcus.substack.com) 
- Cory Doctrow (https://pluralistic.net) 
- Luke Kanies (https://lukekanies.com) 
- Marcus Hutchins (https://malwaretech.com/2025/08/every-reason-why-i-hate-ai.html) 
- Dr. Timnet Gebru’s paper (https://s10251.pcdn.co/pdf/2021-bender-parrots.pdf) 
- James Fodor (https://arxiv.org/abs/2502.14318) 
- Why Models Hallucinate https://openai.com/index/why-language-models-hallucinate
- Paolo Perrone https://theaiengineer.substack.com/p/why-is-inference-slow-and-expensive
- Model Drift (https://www.ibm.com/think/topics/model-drift)
- Context Rot (https://www.understandingai.org/p/context-rot-the-emerging-challenge)
- LLM Benchmarking (https://blog-datalab.com/making-sense-of-ai-benchmarks/)



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
</style>

{{< /css.inline >}}
