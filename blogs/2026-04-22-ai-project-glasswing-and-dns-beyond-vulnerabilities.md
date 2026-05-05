---
title: "AI, Project Glasswing and DNS: Beyond Vulnerabilities"
url: "https://www.infoblox.com/blog/security/ai-project-glasswing-and-dns-beyond-vulnerabilities/"
date: "Wed, 22 Apr 2026 12:55:26 +0000"
author: "Craig Sanderson"
feed_url: "https://www.infoblox.com/blog/feed/"
---
<p><img alt="" class="attachment-post-thumbnail size-post-thumbnail wp-post-image" height="408" src="https://www.infoblox.com/blog/wp-content/uploads/ai-project-glasswing-dns-thumbnail.jpeg" width="612" /></p><p>Project Glasswing is a genuine step change in cybersecurity. Anthropic’s Claude Mythos Preview model has reportedly uncovered <strong>thousands of previously unknown vulnerabilities</strong> across major operating systems, browsers and critical software, including a 27‑year‑old OpenBSD bug, a 16‑year‑old FFmpeg flaw and chained exploits in the Linux kernel that lead to full system compromise. It is powerful enough that Anthropic has decided not to release the full Mythos model broadly, positioning Glasswing as a tightly controlled, “defense‑first” initiative with a limited consortium of hyperscalers, security vendors and financial institutions.</p>
<p>So, is the glass half full or half empty?</p>
<ul class="list-spacing">
<li><strong>Glass Half Full</strong>: Defenders finally have AI that can find and help fix vulnerabilities at machine speed.</li>
<li><strong>Glass Half Empty</strong>: The same class of capability will eventually be in the hands of attackers, compressing the time from discovery to weaponization to minutes, not months.</li>
</ul>
<p>Both are true. But focusing only on vulnerabilities misses a bigger problem: the world is already full of <strong>exposed configuration mistakes</strong> that today’s understaffed security teams struggle to find and fix.</p>
<p>And AI will accelerate the exploitation of those just as surely as it accelerates vulnerability discovery.</p>
<h3>The Real Bottleneck Isn’t Just Patching—It’s Everything Around It</h3>
<p>Most critical infrastructure and government environments are already behind on patching for entirely understandable reasons: legacy systems, fragile integration chains and change windows negotiated with business owners who fear outages more than Common Vulnerabilities and Exposures (CVE). Even if Mythos‑class models hand defenders a perfectly prioritized list of zero‑days, many organizations <strong>cannot patch fast enough</strong> to keep up.</p>
<p>But underneath the vulnerability backlog is something even more basic:</p>
<ul class="list-spacing">
<li><strong>Secure configuration management at scale</strong>—across DNS, identity, network, cloud, OT and application stacks—is still largely manual and error‑prone.</li>
<li>Security teams are <strong>chronically understaffed</strong>, while being pressed to “move at the speed of the business.” The result is predictable: shortcuts, drift and blind spots.</li>
</ul>
<p>In DNS alone, we see this every day. In a recent assessment of nine major corporations, every single one had DNS misconfigurations that could be exploited. Two had <strong>critical exposures that would be trivial for a competent threat actor to use</strong>. None of these issues required a zero‑day; they were the outcome of ordinary operational pressure over time.</p>
<h3>DNS as the Canary: Lame Delegations, NIST SP 800‑81 and Sitting Ducks</h3>
<p>DNS is a perfect example of why “vulnerabilities versus misconfigurations” is a false dichotomy.</p>
<p><strong>National Institute of Standards and Technology (NIST) Special Publication (SP) 800‑81</strong> has only recently been updated after years of relatively static guidance, reflecting a growing recognition that DNS is a critical security control, not just plumbing. The refreshed guidance sharpens expectations around architecture, logging and controls for issues such as lame delegations, dangling records and abuse of recursive resolvers, and is rapidly becoming the baseline for DNS security best practice, including in the European Union’s <strong>NIS2</strong> technical guidance on DNS and protective DNS controls. It is the reference many regulators and operators reach for when they ask, “What does secure DNS actually mean in practice?” At the same time, recent campaigns such as the <strong>Sitting Ducks</strong> hijacks by Russian‑nexus actors like Vacant Viper and the broader “Vipers” and “Hawks” crews—which have abused misconfigured name‑server delegations and other DNS hygiene failures to hijack tens of thousands of domains, including household brands—underline how far real‑world practice still lags this guidance.</p>
<p>Infoblox and Eclypsium’s <strong>Sitting Ducks</strong> research showed that simple DNS misconfigurations, especially <strong>lame delegations</strong>, allow attackers to hijack domains without ever touching the registrar account. At any given time, over <strong>one million domains are exploitable</strong>; hundreds are actively hijacked every day. Follow‑on work found roughly <strong>800,000 vulnerable domains and about 70,000 confirmed hijacks</strong>, driven primarily by misconfigured name server settings. Other studies estimate that on the order of <strong>10 to 14 percent of delegations are lame</strong> in large domain samples.</p>
<p>Those same research threads, and subsequent Infoblox work, highlight how:</p>
<ul class="list-spacing">
<li><strong>Dangling CNAMEs</strong> and other dangling DNS records are pervasive, leaving “forgotten” links to expired cloud resources or domains that attackers can reclaim for phishing, malware delivery and traffic distribution systems (TDSs).</li>
<li>Misconfigurations like lame delegations are <strong>not assigned CVEs</strong> and often sit outside the vulnerability management process entirely, so agencies and enterprises systematically under‑prioritize them compared to software bugs.</li>
</ul>
<p>In other words, the world doesn’t just have a <strong>vulnerability problem</strong>. It has a <strong>configuration hygiene problem</strong> on top of that, and the latter is at least as attractive to attackers, precisely because it is so often invisible to defenders.</p>
<p>Now imagine Mythos‑class models and their successors applied not only to code, but to DNS zones, cloud control planes, routing policies and identity and access management (IAM) graphs. They won’t just find zero‑days; they’ll find <strong>every misconfiguration that matters</strong> and automatically chain them into practical attack paths.</p>
<h3>Why We Need an AI Automation Strategy for Both Vulnerabilities and Configurations</h3>
<p>If you accept that:</p>
<ol class="list-spacing">
<li>AI will make <strong>discovering exploitable conditions (bugs and misconfigs) cheap and fast</strong>, and</li>
<li>You <strong>cannot rely on vendors always shipping a patch in time</strong>, nor on your own organization always having a convenient maintenance window, then the response cannot simply be “patch faster.” </li>
</ol>
<p>Organizations need a <strong>holistic AI‑driven automation strategy</strong> that treats vulnerabilities and configurations as part of the same risk fabric:</p>
<p><strong>1. Unify Visibility and Risk Modeling</strong></p>
<ul class="list-spacing">
<li>Correlate software vulnerabilities with DNS hygiene, cloud posture, network exposure and identity misconfigurations into a single view of “ways an attacker can win.”</li>
<li>Include external attack surface and DNS risks like lame delegation, Sitting Ducks conditions and dangling CNAMEs alongside traditional CVEs.</li>
</ul>
<p><strong>2. Use AI To <em>Discover</em> and <em>Prioritize</em> Issues, Not Just To Scan Code</strong></p>
<ul class="list-spacing">
<li>Continuously analyze configs, logs and external DNS data to highlight misconfigurations that materially expand blast radius, not just “non‑compliant” settings.</li>
<li>Ask models to reason about <strong>attack paths</strong>: “Given this set of DNS, network and identity issues, what’s the shortest route to domain admin or data theft?”</li>
</ul>
<p><strong>3. Automate Mitigation—Especially when Patching Isn’t Possible</strong></p>
<p>You won’t always get a vendor patch in time, and even when you do, you won’t always have the change window to deploy it. That’s where AI‑assisted automation and policy come in:</p>
<ul class="list-spacing">
<li>For <strong>DNS</strong>: Automatically detect and remediate lame delegations, clean up dangling records and enforce safe delegation patterns with minimal human approval.</li>
<li>For <strong>Network and Identity</strong>: Automatically tighten segmentation, DNS and web filtering, and access controls around assets affected by high‑risk vulnerabilities or misconfigurations.</li>
<li>For <strong>Applications and Cloud</strong>: Generate and deploy safe, reversible configuration changes (e.g., disabling risky plugins, tightening security groups, revoking stale trust relationships) under human‑defined guardrails.</li>
</ul>
<p>The goal is not “no humans,” but <strong>no heroics</strong>: let humans decide strategy and exceptions, while AI does the drudge work of detection, enrichment, change generation and verification.</p>
<p><strong>4. Bake Safety and Governance into the AI Layer Itself</strong></p>
<ul class="list-spacing">
<li>Treat powerful security models as <strong>high‑risk infrastructure</strong>, with their own access controls, logging and red‑team testing.</li>
<li>Ensure AI‑driven automations are explainable, reversible and tested in staging before touching production.</li>
</ul>
<h3>Planning for the Dam to Break—and a Concrete First Step</h3>
<p>Anthropic is trying to be responsible in how it exposes Mythos‑class capability, and that’s commendable. But we should be honest: <strong>hoping that one vendor “holds the line” is not a strategy</strong>.</p>
<p>History tells us that:</p>
<ul class="list-spacing">
<li>Capabilities leak and are replicated. Rivals are already racing to match or surpass Mythos in cyber‑relevant skills.</li>
<li>Governments and critical infrastructure will <strong>not</strong> all be invited into closed initiatives like Glasswing. Most of the world’s vulnerable infrastructure will remain outside that inner circle for a long time.</li>
</ul>
<p>At some point, the dam breaks: Mythos‑class offensive capability, or something close enough, will be broadly available. When that happens, attackers won’t need deep expertise to find exploitable DNS misconfigurations, dangling CNAMEs, legacy protocol exposures or unpatched zero‑days. They’ll ask their AI, and it will oblige.</p>
<p>The only sustainable response is for defenders to <strong>embrace the same level of automation and intelligence</strong>, and to point it not just at software vulnerabilities but at the sprawling universe of configuration risk that makes those vulnerabilities so devastating.</p>
<p>AI will absolutely help us find and fix more bugs. But if we want the glass to be more than half full, we have to use it to clean up the misconfigurations too, starting with an honest DNS health check against baselines like NIST SP 800‑81 and NIS2 guidance, and then building an <strong>AI‑assisted operations strategy</strong> that continuously enforces that hygiene.</p>
<p>A practical first step is to use <a href="https://info.infoblox.com/sec-en-inspectsecurity-registration.html"><strong>Infoblox Inspect</strong></a> to assess how well your current DNS infrastructure and security controls actually protect you. Infoblox Inspect is a lightweight, complimentary assessment that:</p>
<ul class="list-spacing">
<li>Validates DNS infrastructure and configuration against best practices</li>
<li>Tests your ability to block high‑risk and malicious domains, including TDS, domain generation algorithms (DGAs), phishing and command-and-control (C2) infrastructure</li>
<li>Surfaces gaps in both security controls and DNS hygiene that attackers routinely exploit</li>
<li>Delivers an executive‑ready report you can map directly to NIST 800‑81 and NIS2‑aligned expectations, and use to drive both remediation and your AI operations roadmap</li>
</ul>
<p>Glasswing and Mythos Preview show us what is now possible—for defenders and for attackers. The question is whether we use the same level of intelligence to finally bring DNS and configuration hygiene up to the standard our critical infrastructure deserves.</p>
<h3 class="footnotes">Public Sources</h3>
<ul class="footnotes-listing">
<li><a href="https://www.anthropic.com/glasswing" target="_blank">Project Glasswing: Securing critical software for the AI era</a></li>
<li><a href="https://www.anthropic.com/project/glasswing" target="_blank">Project Glasswing</a></li>
<li><a href="https://blogs.infoblox.com/threat-intelligence/who-knew-domain-hijacking-is-so-easy/">Who Knew? Domain Hijacking is So Easy</a>. Infoblox Threat Intel. Infoblox. July 31, 2024.</li>
<li><a href="https://www.techtarget.com/searchsecurity/news/366615752/Infoblox-800000-domains-vulnerable-to-hijacking-attack" target="_blank">Infoblox: 800,000 domains vulnerable to hijacking attack</a>. Waldman, Ariel. Informa TechTarget. November 14, 2024.</li>
<li><a href="https://www.infosecurity-magazine.com/news/sitting-ducks-dns-attacks-global/" target="_blank">Sitting Ducks DNS Attacks Put Global Domains at Risk</a>. Mascellino, Alessandro. Infosecurity Magazine. November 14, 2024.</li>
<li><a href="https://eclypsium.com/blog/ducks-now-sitting-dns-internet-infrastructure-insecurity/" target="_blank">Ducks Now Sitting (DNS): Internet Infrastructure Insecurity</a>. Eclypsium. July 31, 2024.</li>
<li><a href="https://www.theregister.com/2024/07/31/domains_with_delegated_name_service/" target="_blank">Russia takes aim at Sitting Ducks domains, bags 30,000+</a>. Claburn, Thomas. The Register. July 31, 2024.</li>
<li><a href="https://securityaffairs.com/166445/hacking/sitting-ducks-attack-technique.html" target="_blank">Sitting Ducks attack exposes over a million domains to hijacking</a>. Paganini, Pierluigi. Security Affairs. August 2, 2024.</li>
<li><a href="https://blogs.infoblox.com/threat-intelligence/dns-predators-hijack-domains-to-supply-their-attack-infrastructure/">DNS Predators Hijack Domains to Supply their Attack Infrastructure</a>. Infoblox Threat Intel. Infoblox. November 14, 2024.</li>
<li><a href="https://www.hpcwire.com/aiwire/2026/04/09/anthropic-unveils-project-glasswing-as-claude-mythos-targets-software-vulnerabilities/" target="_blank">Anthropic Unveils ‘Project Glasswing’ as Claude Mythos Targets Software Vulnerabilities</a>. AIwire. April 9, 2026.</li>
</ul>

<p><span class="gradient"></span></p>
		<div class="wpulike wpulike-default "><div class="wp_ulike_general_class wp_ulike_is_restricted"><button class="wp_ulike_btn wp_ulike_put_image wp_post_btn_13352" type="button"></button><span class="count-box wp_ulike_counter_up"></span>			</div></div>
	<p>The post <a href="https://www.infoblox.com/blog/security/ai-project-glasswing-and-dns-beyond-vulnerabilities/">AI, Project Glasswing and DNS: Beyond Vulnerabilities</a> appeared first on <a href="https://www.infoblox.com/blog">Infoblox Blog</a>.</p>
