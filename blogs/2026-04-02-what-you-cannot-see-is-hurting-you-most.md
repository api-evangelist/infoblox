---
title: "What You Cannot See is Hurting You Most"
url: "https://www.infoblox.com/blog/company/what-you-cannot-see-is-hurting-you-most/"
date: "Thu, 02 Apr 2026 13:55:27 +0000"
author: "Mehul Patel"
feed_url: "https://www.infoblox.com/blog/feed/"
---
<p><img alt="" class="attachment-post-thumbnail size-post-thumbnail wp-post-image" height="408" src="https://www.infoblox.com/blog/wp-content/uploads/what-you-cannot-see-is-hurting-you-most-thumbnail.jpg" width="612" /></p><p>I was on a call last week with a vice president of IT operations who confidently told me their infrastructure visibility was “probably 85 percent, maybe 90 percent.” When I asked how they measured that, there was a pause. “Well, we run network scans weekly, we have got endpoint agents on most systems and our CMDB is … reasonably up to date.”</p>
<p>Two weeks later, they ran Infoblox Universal Asset Insights<img alt="™" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2122.png" style="height: 1em;" /> across their environment.</p>
<p>It found 48 percent more assets than all their existing tools combined.</p>
<p>Their real number? 52 percent.</p>
<p>They found 847 IoT devices their scanning tools had never detected: cloud resources that had been decommissioned months ago but were still running (and billing), and shadow IT deployments nobody owned. The gap between what they thought they could see and what actually existed was not a rounding error. It was a business risk.</p>
<p>Here is what bothered me most: this was not unusual. According to Gartner research, only 17 percent of organizations can clearly identify 95 percent or more of their assets.<sup>1</sup> The rest are operating with significant blind spots—and most do not realize it.</p>
<h3>The Intelligence Already Exists</h3>
<p>Most organizations approach infrastructure visibility as a data collection problem. They deploy more scanners, add more agents and integrate more tools, trying to build visibility by aggregating partial views from dozens of sources.</p>
<p>But there is a different approach, and it starts with recognizing something fundamental: for on-premises infrastructure, every device that connects must interact with your network’s DNS and DHCP services.</p>
<ul class="list-spacing">
<li>Request an IP address → DHCP assigns and tracks every allocation</li>
<li>Resolve domain names → DNS logs every lookup and connection</li>
<li>Be mapped to location → IP address management (IPAM) tracks network topology</li>
</ul>
<p>For on-premises environments, nothing bypasses DNS and DHCP. Your network services see every connection because devices cannot function without them. For cloud environments, Universal Asset Insights extends this authoritative foundation through direct integration with cloud provider APIs, capturing resources the moment they’re provisioned.</p>
<p>DNS and DHCP are not visibility tools you deploy. They are the operational network services that already see everything on-prem by default. Universal Asset Insights leverages this foundation and extends it systematically across hybrid and multi-cloud environments.</p>
<p>This data is authoritative because it is operational. On-premises networks require DNS and DHCP to function. Cloud platforms expose real-time provisioning data through their APIs. Every connection is recorded. Every transaction is logged. Every change is tracked, in real time.</p>
<p>But here’s what most organizations miss: raw DNS and DHCP transaction logs aren’t infrastructure intelligence—they’re unprocessed data. A DHCP lease shows an IP was assigned, not what device received it or whether it’s authorized. DNS queries show lookups, not asset relationships or security context.</p>
<p>The organizations that solve the discovery confidence gap don’t just collect authoritative data. They process it at scale, enrich it with cloud provider APIs, apply enhanced discovery for edge cases and correlate everything into unified intelligence. That’s the difference between having visibility and insights.</p>
<h3>Why This Matters More Than Ever</h3>
<p>I have been thinking about why organizations tolerate partial visibility. The reasons usually sound reasonable:</p>
<ul class="list-spacing">
<li>We are at 80–90% coverage—that is good enough</li>
<li>We will improve visibility during the next tool refresh</li>
<li>Scanning tools will eventually find everything</li>
<li>This is an acceptable level of risk</li>
</ul>
<p>These assumptions made sense five years ago. They do not make sense now.</p>
<p>Gartner research shows that 30 percent of IT assets are lost or unaccounted for.<sup>2</sup> When your asset inventory has that kind of gap, the consequences compound: compliance audits become guesswork, security tools cannot protect what they do not know exists and cloud resources run untracked.</p>
<p>According to the Flexera State of Cloud report, 28 percent of annual public cloud spend is wasted,<sup>3</sup> much of it on orphaned resources and untracked infrastructure. For a mid-sized organization spending $3–5 million annually on cloud, that is nearly $1 million in waste.</p>
<p>But here is what changes the equation completely: AI and automation.</p>
<p>Organizations are accelerating AI adoption, but AI cannot secure what it cannot see. AI agents and automation frameworks require accurate, verified asset information to make reliable decisions. Industry data shows that typical CMDB accuracy hovers around 60 percent.<sup>4</sup> When your configuration database is 60 percent accurate, your AI operates with 40 percent blind spots.</p>
<p>Incomplete discovery data trains models on flawed inputs. Automation built on partial visibility generates cascading failures. Agentic AI makes decisions about assets that do not exist—and misses assets that do.</p>
<p>Artificial intelligence does not create a visibility problem. It magnifies it. <a href="https://www.infoblox.com/resources/ebook/one-reality/" target="_blank">Check out the e-book</a> to understand the risks—and learn how authoritative network intelligence is the foundation AI actually needs.</p>
<h3>What Actually Works</h3>
<p>Over the last year, I have watched customers solve this problem, not by adding more scanning tools, but by changing where they look for truth.</p>
<p>A global financial services organization was managing AWS, Azure and Google Cloud independently—no unified view of IP allocation, ownership or resource inventory. They discovered 847 orphaned cloud resources and eliminated significant annual waste. Time to full multi-cloud visibility? 15 minutes.</p>
<p>A UK supermarket chain facing a £6.8 billion IT divestiture needed to separate infrastructure within 36 months or face regulatory fines. They used DNS and DHCP intelligence as the foundation for the entire separation. Met the deadline. Avoided the fines.</p>
<p>An enterprise technology company had thousands of dangling DNS records exposing them to domain takeover attacks. They identified and remediated 2,400 inactive DNS records, reducing their attack surface vulnerability by 40 percent.</p>
<h3>Why Some Organizations Achieve Complete Visibility</h3>
<p>Traditional scanning tools face inherent limitations:</p>
<ul class="list-spacing">
<li>Scan periodically, missing devices between intervals</li>
<li>Require agents that IoT/OT devices cannot run</li>
<li>Miss ephemeral workloads that exist for minutes</li>
<li>Cannot track disconnected or sleeping systems</li>
</ul>
<p>Universal Asset Insights uses a multi-layer architecture that eliminates these gaps:</p>
<ul class="list-spacing">
<li><strong>On-premises infrastructure</strong> (servers, workstations, network devices)
<ul class="list-spacing">
<li>Foundation: DNS/DHCP transaction logs capture every connection in real time</li>
</ul>
</li>
<li><strong>Multi-cloud environments</strong> (AWS, Azure, Google Cloud, private cloud)
<ul class="list-spacing">
<li>Extended via: Cloud provider APIs processed at scale and normalized into actionable IPAM intelligence</li>
</ul>
</li>
<li><strong>Edge and IoT ecosystems</strong> (medical devices, industrial control, sensors)
<ul class="list-spacing">
<li>Foundation: DNS/DHCP sees every network connection; enhanced discovery captures static IP devices</li>
</ul>
</li>
<li><strong>Shadow IT and BYOD</strong> (unmanaged endpoints, contractor devices)
<ul class="list-spacing">
<li>Foundation: DNS/DHCP logs every network request regardless of endpoint management status</li>
</ul>
</li>
<li><strong>Ephemeral workloads</strong> (containers, serverless, auto-scaling instances)
<ul class="list-spacing">
<li>Extended via: Cloud API integration captures instances that exist for minutes</li>
</ul>
</li>
</ul>
<p>This multi-layer architecture delivers 100 percent coverage versus 60–70 percent from scanning-based tools. The DNS/DHCP foundation guarantees visibility into everything that connects to on-premises networks. Cloud API integration extends that foundation to hybrid and multi-cloud environments. Enhanced discovery engines catch edge cases like static IP devices. Machine learning correlation ties it all together into a unified, normalized view.</p>
<p>Where traditional approaches aggregate fragmented data sources and hope for coverage, the organizations solving this problem start with authoritative network services and extend systematically.</p>
<h3>Three Infrastructure Truths</h3>
<p>When organizations build from an authoritative foundation across on-prem and cloud environments, they unlock three capabilities that eliminate blind spots:</p>
<ul class="list-spacing">
<li><strong>Authoritative IPAM Intelligence</strong>: Complete, real-time IP address management across hybrid and multi-cloud environments. Eliminate IP conflicts, reduce MTTR by 70%, accelerate cloud migrations.</li>
<li><strong>Verified CMDB Accuracy</strong>: ServiceNow CMDB updated with verified asset data—95%+ accuracy, up from typical 60%. Save 16+ hours monthly on manual reconciliation, enable reliable automation, pass compliance audits.</li>
<li><strong>Security Context and Exposure Mapping</strong>: Real-time asset context for SIEM/SOAR correlation. Reduce incident MTTR by 75%, eliminate false positives, close security blind spots.</li>
</ul>
<p>When NetOps, SecOps and CloudOps work from a single DNS and DHCP-based source of truth, they speak the same operational language. Incidents do not linger because teams debate which data is correct. Diagnostics happen faster. Triage becomes systematic.</p>
<h3>What I Have Learned</h3>
<p>I used to think infrastructure visibility was a better discovery tool. What I have learned is that it is actually about recognizing the truth.</p>
<p>The infrastructure intelligence you need already exists. It is in the DNS and DHCP services your infrastructure depends on to function. Every device that connects leaves an authoritative record. Every connection is tracked. Every change is logged.</p>
<p>The question is not whether complete visibility is possible. The question is how much you are losing while operating with partial truth.</p>
<p>Because if you are making decisions about security, compliance, operations or cloud spending based on data that is 30–40 percent incomplete, you are not making informed decisions. You are guessing.</p>
<p>And eventually, those guesses catch up with you, especially when AI starts amplifying them.</p>
<h3 style="font-size: 18px;">Sources</h3>
<ol style="font-size: 14px;">
<li><em>What You Need to Know from Gartner Innovation Insight: Attack Surface Management</em>, Le, Jon, JupiterOne, June 24, 2024.<br /><a href="https://www.jupiterone.com/blog/what-you-need-to-know-from-gartner-innovation-insight-attack-surface-management" target="_blank">https://www.jupiterone.com/blog/what-you-need-to-know-from-gartner-innovation-insight-attack-surface-management</a></li>
<li><em>Gartner Bombshell: 30% of IT Assets Lost</em>, Marks, Kyle, Retire-IT. Last accessed: February 5, 2026.<br /><a href="https://retire-it.com/gartner-ham-bombshell/" target="_blank">https://retire-it.com/gartner-ham-bombshell/</a></li>
<li><em>Public Cloud Waste at 28%: Time to Consider On-Demand Private Cloud as an Alternative?</em>, Ghosh, Sash, OpenMetal, October 23, 2025.<br /><a href="https://openmetal.io/resources/blog/control-public-cloud-waste-with-alternative-cloud/" target="_blank">https://openmetal.io/resources/blog/control-public-cloud-waste-with-alternative-cloud/</a></li>
<li><em>CMDB Accuracy Woes? It’s Time for a New Approach</em>, Deur, Paul, ReadyWorks. Last accessed: February 5, 2026.<br /><a href="https://www.readyworks.com/blog/cmdb-accuracy-woes-its-time-for-a-new-approach" target="_blank">https://www.readyworks.com/blog/cmdb-accuracy-woes-its-time-for-a-new-approach</a></li>
</ol>

<p><span class="gradient"></span></p>
		<div class="wpulike wpulike-default "><div class="wp_ulike_general_class wp_ulike_is_restricted"><button class="wp_ulike_btn wp_ulike_put_image wp_post_btn_13249" type="button"></button><span class="count-box wp_ulike_counter_up"></span>			</div></div>
	<p>The post <a href="https://www.infoblox.com/blog/company/what-you-cannot-see-is-hurting-you-most/">What You Cannot See is Hurting You Most</a> appeared first on <a href="https://www.infoblox.com/blog">Infoblox Blog</a>.</p>
