---
title: "Don’t Wait To Be Attacked: Stop Phishing, C2 and Data Exfiltration with Infoblox Threat Intelligence in AWS Network Firewall"
url: "https://www.infoblox.com/blog/security/infoblox-managed-rules-aws-network-firewall-ga/"
date: "Thu, 23 Apr 2026 15:00:03 +0000"
author: "Ben Fischer"
feed_url: "https://www.infoblox.com/blog/feed/"
---
<p><img alt="" class="attachment-post-thumbnail size-post-thumbnail wp-post-image" height="408" src="https://www.infoblox.com/blog/wp-content/uploads/infoblox-pmr-aws-thumbnail.jpeg" width="612" /></p><p>Security teams running <strong>AWS Network Firewalls</strong> are under constant pressure. Attacks keep getting more sophisticated, faster and automated, while teams and budgets do not. According to IBM’s <strong>2024 Cost of a Data Breach Report</strong>, the <strong>average global cost of a data breach reached USD 4.88 million</strong>, a 10 percent increase over the prior year, and the largest jump since the COVID-19 pandemic began.<sup>1</sup> At the same time, multiple studies indicate that <strong>over 90 percent of cyberattacks begin with phishing</strong>, and that attackers increasingly rely on domain-centric infrastructure for command and control (C2) and data theft.<sup>2,3</sup></p>
<p>AWS has responded by making managed rules from AWS Marketplace available directly in AWS Network Firewall,<sup>4</sup> so customers can quickly add curated protections from trusted partners without extra infrastructure or complexity. This <strong>moves security controls closer to the edge of your AWS environment</strong>, rather than relying only on downstream detection tools, and <strong>even small, incremental improvements at the edge compound into sizeable reductions in both breach likelihood and impact by:</strong></p>
<ul class="list-spacing">
<li><strong>Stops more threats before they ever touch workloads</strong></li>
<li><strong>Shifts security from reactive cleanup to preemptive blocking</strong></li>
<li><strong>Reduces the cost and complexity of dealing with compromises later in the stack</strong></li>
</ul>
<p>Building on that foundation, <a href="https://aws.amazon.com/marketplace/pp/prodview-m7vgh7okmokzm" target="_blank"><strong>Infoblox Managed Rules for AWS Network Firewall</strong></a> are now available for free as an Expanded Free Preview. Together, AWS and Infoblox give customers a <strong>preemptive, Protective DNS layer</strong> that helps stop phishing, C2 and data exfiltration <strong>before</strong> they impact AWS workloads.</p>
<h3>What’s in It for You as an AWS Network Firewall Customer</h3>
<p>With <a href="https://aws.amazon.com/marketplace/pp/prodview-m7vgh7okmokzm" target="_blank"><strong>Infoblox Managed Rules</strong></a> enabled in AWS Network Firewall, you can:</p>
<ul class="list-spacing">
<li><strong>Block high-risk domains before connections are made.</strong><br />Reduce successful phishing sessions, credential theft and C2 callbacks by enforcing decisions at the domain layer instead of waiting for downstream alerts.</li>
<li><strong>Cut incident volume and noise for your security operations center (SOC).</strong><br />Prevent many attacks from ever reaching endpoints or downstream tools, so your team spends less time chasing avoidable alerts and more time on high-value investigations.</li>
<li><strong>Improve time-to-protection with AWS-native simplicity.</strong><br />Subscribe, enable and monitor curated rule groups directly in the <strong>AWS Network Firewall console</strong>, with no new appliances or agents to deploy.</li>
<li><strong>Strengthen defense in depth in line with AWS best practices.</strong><br />Add <strong>DNS-layer security</strong> at the firewall to complement existing AWS Network Firewall policies, AWS Managed Rules and partner managed rules. This aligns with the <strong>Security Pillar of the </strong><a href="https://aws.amazon.com/architecture/well-architected/" target="_blank"><strong>AWS Well-Architected Framework</strong></a>, which recommends multiple, mutually reinforcing controls around critical workloads.</li>
<li><strong>Scale protection automatically as your AWS footprint grows.</strong><br />As you add virtual private clouds (VPCs), regions and traffic, curated Suricata-compatible rule groups and automated feed updates scale with you without multiplying manual rule maintenance.</li>
<li><strong>Enable best-of-breed protection DNS security (Infoblox) directly in the AWS console</strong> without needing to traverse back and forth between Marketplace and AWS console.</li>
<li><strong>Easily validate the security effectiveness</strong> by trying the solution without a big upfront commitment.</li>
<li><strong>Enjoy consumption-based pricing</strong> to match cloud purchasing and billing models.</li>
</ul>
<h3>Why DNS-Based, Preemptive Blocking Matters</h3>
<p>Every phishing click, C2 callback and domain-based exfiltration attempt depends on <strong>DNS</strong>. That makes the DNS the earliest and most universal signals of malicious intent.</p>
<p>Independent research and DNS-focused reports highlight that:</p>
<ul class="list-spacing">
<li>Phishing remains a leading initial attack vector, responsible for a significant share of breaches and user-initiated incidents. For example, StationX data summarized by Paubox<sup>2</sup> shows that <strong>91 percent of all cyberattacks begin with a phishing email</strong> and an estimated <strong>3.4 billion phishing emails</strong> are sent every day.</li>
<li>DNS is routinely abused for tunneling, C2 and exfiltration, and is a critical layer to secure in modern architectures.<sup>5,6</sup></li>
</ul>
<p>This is why Protective DNS and DNS-layer security are becoming core parts of cloud security programs. By enforcing <strong>predictive, DNS-based threat intelligence</strong> and decisions at your AWS Network Firewalls, you can:</p>
<ul class="list-spacing">
<li>Block known and predicted malicious domains before workloads or users connect.</li>
<li><strong>Cut off entire clusters of attacker infrastructure that sit behind those domains, even as IPs and URLs change, so you catch fast-moving, domain-driven campaigns that IP or URL-only controls often miss.</strong></li>
<li>Reduce the number of attacks that reach endpoints, web proxies or security information and event management (SIEM), lowering the cost and time of cleaning them up later.</li>
</ul>
<p>In other words, you move from reactive detection to <strong>preemptive, domain-centric control</strong> at a high-leverage point in your AWS environment.</p>
<h3>What Infoblox Managed Rules for AWS Network Firewall Are</h3>
<p><strong>Infoblox Managed Rules for the AWS Network Firewall</strong> deliver <strong>curated rule groups</strong> that you enable natively within the AWS Network Firewall console.<sup>7</sup></p>
<p>These rule groups are:</p>
<ul class="list-spacing">
<li><strong>Powered by Infoblox Predictive DNS Threat Intelligence</strong><br />Built from rich DNS telemetry, leveraging millions of indicators and years of DNS focused research to identify malicious and high-risk domains earlier in the kill chain.</li>
<li><strong>Focused on High-Impact Protections</strong>
<ul class="list-spacing">
<li>Phishing and credential theft</li>
<li>C2 communications</li>
<li>DNS and domain-based data exfiltration</li>
</ul>
</li>
<li><strong>Continuously and Automatically Updated</strong><br />Curated rule groups that include millions of malicious domains that are automatically refreshed as attacker infrastructure changes, so customers stay protected without having to hand edit or tune domain level rules.</li>
<li><strong>Delivered as Suricata-Compatible Rule Groups</strong><br />Tuned specifically for use in AWS Network Firewall policies, alongside AWS-native and other partner rules.</li>
</ul>
<p>You get all of this through an <strong>AWS-native experience</strong>. You use tools you already know, such as AWS Network Firewall and AWS Marketplace for preemptive protection behind the scenes.</p>
<p><img alt="Figure 1" src="https://www.infoblox.com/blog/wp-content/uploads/infoblox-pmr-aws-figure1.jpeg" /></p>
<p class="image-caption">Figure 1. AWS Network Firewall deployment protecting an AWS Virtual Private Cloud (VPC)</p>
<h3>How It Works in AWS Network Firewall</h3>
<p>From a customer’s point of view, enabling Infoblox Managed Rules is straightforward:</p>
<ol class="list-spacing">
<li><strong>Subscribe via AWS Marketplace</strong>
<ol class="list-spacing lower-alpha">
<li>In the <strong>AWS Network Firewall console</strong>, go to <strong>Managed rules from the AWS Marketplace</strong>.</li>
<li>Subscribe to <a href="https://aws.amazon.com/marketplace/pp/prodview-m7vgh7okmokzm" target="_blank"><strong>Infoblox Managed Rules AWS Network Firewall</strong></a> and select the desired rule groups in the AWS Marketplace listing.</li>
</ol>
</li>
<li><strong>Attach to existing firewall policies</strong><br />Associate Infoblox Managed Rules with AWS Network Firewall policies that protect:
<ul class="list-spacing">
<li><strong>Internet facing traffic</strong> (north-south)</li>
<li><strong>VPC to VPC and hybrid traffic</strong> (east-west, via transit gateways and inspection VPCs)</li>
</ul>
</li>
<li><strong>Monitor and tune with AWS-native logging</strong>
<ol class="list-spacing lower-alpha">
<li>Use <strong>AWS Network Firewall logging</strong> to see when Infoblox rules trigger and where they are blocking or alerting.</li>
<li>Forward logs to <strong>Amazon CloudWatch</strong>, S3 and your SIEM or security orchestration, automation and response (SOAR), so they fit into your existing investigation and automation workflows.</li>
</ol>
</li>
</ol>
<p>There is <strong>no new hardware to rack, no agents to deploy and no custom rule language to learn</strong>. AWS manages the lifecycle of managed rules in the firewall, while Infoblox keeps the rule groups and DNS intelligence current.</p>
<h3>Two Concrete Ways Customers Benefit</h3>
<h4>1. Fewer Successful Phishing and Credential-Theft Incidents</h4>
<p>Phishing continues to dominate cybercrime statistics. As noted earlier, StationX data summarized by Paubox<sup>2</sup> shows that <strong>91 percent of cyberattacks begin with phishing</strong>, and an estimated <strong>3.4 billion phishing emails are sent daily</strong>.</p>
<p>With Infoblox Managed Rules active in AWS Network Firewall, when a user, workload or third-party service in AWS attempts to reach a domain known or predicted to be part of a phishing campaign, the firewall can <strong>block that traffic before any sensitive data is submitted</strong>.</p>
<p>This protects:</p>
<ul class="list-spacing">
<li>End users, such as developers or admins accessing AWS resources</li>
<li>Cloud-hosted web applications and APIs</li>
<li>Backend services that might follow links or redirect automatically</li>
</ul>
<p><strong>Customer Value:</strong> Fewer stolen credentials, compromised cloud identities and high-urgency incidents for your security and cloud teams</p>
<h4>2. Disrupted C2 Channels and Lateral Movement</h4>
<p>Once adversaries gain a foothold, they typically establish <strong>C2 channels</strong> to coordinate movement and payloads. These channels are often built on rapidly changing, domain-centric infrastructure.</p>
<p>Infoblox Managed Rules help by:</p>
<ul class="list-spacing">
<li><strong>Blocking outbound domain-based connections</strong> to C2 infrastructure identified by Infoblox predictive intelligence</li>
<li><strong>Preventing beacons, remote tooling downloads and other C2 behavior</strong> at the network perimeter, often before endpoint or log-based tools would have enough evidence to raise an alert</li>
</ul>
<p><strong>Customer Value:</strong> Attackers lose the communication path they rely on for persistence and lateral movement. That reduces both dwell time and the scope of potential compromise in your AWS environment.</p>
<h3>How This Fits into a Broader AWS Security Strategy</h3>
<p>AWS has steadily evolved the AWS Network Firewall to support greater <strong>defense in depth at the cloud network perimeter</strong>, and managed rules from AWS Marketplace are a natural extension of that vision.<sup>4</sup> Infoblox Managed Rules align with this approach by:</p>
<ul class="list-spacing">
<li>Delivering <strong>Protective DNS capabilities as an AWS Network Firewall managed rule option</strong>, right alongside AWS-authored and other partner-authored rules</li>
<li>Giving customers more choice to layer in <strong>specialized DNS-based protections</strong> without leaving the AWS management plane or changing their deployment models</li>
<li>Reinforcing best practices from the <a href="https://aws.amazon.com/architecture/well-architected/" target="_blank"><strong>AWS Well-Architected Framework Security Pillar</strong></a>, which emphasizes multiple, mutually reinforcing controls around critical workloads</li>
</ul>
<h3>Additional Value for Existing Infoblox Threat Defense<img alt="™" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2122.png" style="height: 1em;" /> Customers</h3>
<p>If you already use <strong>Infoblox Threat Defense</strong> or other Infoblox Protective DNS capabilities across on-premises, branch or multi-cloud environments, Infoblox Managed Rules for AWS Network Firewall help you:</p>
<ul class="list-spacing">
<li><strong>Extend the Same Predictive DNS Intelligence into AWS Network Firewall</strong><br />The same signal that powers resolver-level enforcement and analytics now drives curated rule groups at the AWS network perimeter.</li>
<li><strong>Build Consistent Policies across Environments</strong><br />Align how you block phishing, C2 and exfiltration domains across enterprise DNS resolvers, hybrid and multi-cloud deployments, and AWS Network Firewall-protected VPCs and transit gateways.</li>
<li><strong>Simplify Operations while Increasing Coverage</strong><br />Use one DNS-centric threat intelligence foundation while AWS Network Firewall provides regionally distributed, cloud native enforcement close to your AWS workloads.</li>
</ul>
<p>For Threat Defense customers with significant AWS footprints, this can be a <strong>low-effort way to expand preemptive protection</strong> while keeping policy and signal sources consistent.</p>
<h3>Getting Started: A Simple Path to Preemptive Protection</h3>
<p>If you are an AWS Network Firewall customer, you can start evaluating Infoblox Managed Rules with a few simple actions:</p>
<ol class="list-spacing">
<li><strong>Visit the AWS Marketplace Listing</strong>
<ol class="list-spacing lower-alpha">
<li><a href="https://aws.amazon.com/marketplace/pp/prodview-m7vgh7okmokzm" target="_blank">Infoblox Managed Rules AWS Network Firewall</a></li>
<li>Review pricing, supported regions and offer details.</li>
</ol>
</li>
<li><strong>Read the Joint Launch Content</strong>
<ul class="list-spacing">
<li>Infoblox blog: <a href="https://www.infoblox.com/blog/security/bringing-predictive-security-to-the-aws-network-perimeter/">Bringing Predictive Security to the AWS Network Perimeter</a></li>
<li>Infoblox press release: <a href="https://www.infoblox.com/news/news-events/press-releases/infoblox-launches-predictive-dns-based-threat-protection-solution-on-aws/">Infoblox Launches Predictive DNS-Based Threat Protection Solution on AWS</a></li>
<li>AWS partner overview: <a href="https://www.infoblox.com/partners/aws/">Infoblox for AWS</a></li>
</ul>
</li>
<li><strong>Enable Infoblox Managed Rules in a Pilot AWS Environment</strong>
<ol class="list-spacing lower-alpha">
<li>Attach Infoblox rule groups to a <strong>non-production</strong> AWS Network Firewall policy.</li>
<li>Start in <strong>alert or log-only mode</strong> for medium- and low-risk categories. Promote high and critical categories to <strong>block</strong> once behavior is validated against your traffic patterns and change processes.</li>
</ol>
</li>
<li><strong>Integrate with Your Existing Observability and SOC Workflows</strong><br />Route AWS Network Firewall logs to CloudWatch, S3 and your SIEM or SOAR so your teams see when Infoblox rules are stopping threats and can build automation around those events.</li>
<li><strong>Plan Your Rollout across Additional VPCs and Regions</strong><br />Once you are comfortable with the behavior and results, extend Managed Rules usage to additional AWS environments, guided by your risk profile and critical workloads.</li>
</ol>
<h3>Moving Ahead with AWS and Infoblox</h3>
<p>As attackers adopt AI, automation and DNS-centric techniques, organizations need security controls that are <strong>equally automated, intelligent and easy to operationalize</strong>. AWS Network Firewall, with support for <strong>managed rules from AWS Marketplace</strong>, gives customers a powerful platform to do exactly that.</p>
<p><strong>Infoblox Managed Rules for the AWS Network Firewall</strong> add a preemptive, Protective DNS layer to that platform. They help you stop phishing, C2 and data exfiltration <strong>earlier, with less effort and in a way that fits naturally into how you already run AWS</strong>.</p>
<p>To learn more or see a deeper architectural walkthrough, visit the AWS Marketplace listing or the Infoblox for AWS partner page, and start exploring how preemptive DNS-based protection can help you get more value from AWS Network Firewall.</p>
<h3 class="footnotes">Footnotes</h3>
<ol class="footnotes-listing">
<li><em>IBM Report: Escalating Data Breach Disruption Pushes Costs to New Highs</em>. IBM Newsroom. July 30, 2024. <a href="https://newsroom.ibm.com/2024-07-30-ibm-report-escalating-data-breach-disruption-pushes-costs-to-new-highs" target="_blank">https://newsroom.ibm.com/2024-07-30-ibm-report-escalating-data-breach-disruption-pushes-costs-to-new-highs</a></li>
<li><em>2024 phishing statistics: Latest figures and trends</em>. Anthoney, Caitlyn. Paubox. August 5, 2024. <a href="https://www.paubox.com/blog/2024-phishing-statistics-latest-figures-and-trends" target="_blank">https://www.paubox.com/blog/2024-phishing-statistics-latest-figures-and-trends</a></li>
<li><em>Statistics on Phishing Attacks</em>. Danielson, Lizzie. Huntress. March 11, 2026. <a href="https://www.huntress.com/phishing-guide/phishing-attack-statistics" target="_blank">https://www.huntress.com/phishing-guide/phishing-attack-statistics</a></li>
<li><em>Simplify cloud security with managed rules from AWS Marketplace for AWS Network Firewall</em>. Parwani, Dhanil. Shah, Amish. AWS Security Blog. November 19, 2025. <a href="https://aws.amazon.com/blogs/security/simplify-cloud-security-with-managed-rules-from-aws-marketplace-for-aws-network-firewall/" target="_blank">https://aws.amazon.com/blogs/security/simplify-cloud-security-with-managed-rules-from-aws-marketplace-for-aws-network-firewall/</a></li>
<li><em>2024 DNS Threat Landscape</em>. Lenaerts, Bart. Grimes, Tom. Infoblox Threat Intel. December 20, 2024. <a href="https://www.infoblox.com/blog/threat-intelligence/2024-dns-threat-landscape/">https://www.infoblox.com/blog/threat-intelligence/2024-dns-threat-landscape/</a></li>
<li><em>The Most Common DNS Security Risks in 2026 (And How to Mitigate Them)</em>. Heimdal. February 8, 2026. <a href="https://heimdalsecurity.com/blog/dns-security-risks/" target="_blank">https://heimdalsecurity.com/blog/dns-security-risks/</a></li>
<li><em>Infoblox Managed Rules from AWS Marketplace for AWS Network Firewall</em> (Infoblox solution note). Infoblox. 2025. <a href="https://insights.infoblox.com/solution-notes/infoblox-solution-note-infoblox-managed-rules-from-aws-marketplace-for-aws-network-firewall" target="_blank">https://insights.infoblox.com/solution-notes/infoblox-solution-note-infoblox-managed-rules-from-aws-marketplace-for-aws-network-firewall</a></li>
</ol>

<p><span class="gradient"></span></p>
		<div class="wpulike wpulike-default "><div class="wp_ulike_general_class wp_ulike_is_restricted"><button class="wp_ulike_btn wp_ulike_put_image wp_post_btn_13343" type="button"></button><span class="count-box wp_ulike_counter_up"></span>			</div></div>
	<p>The post <a href="https://www.infoblox.com/blog/security/infoblox-managed-rules-aws-network-firewall-ga/">Don’t Wait To Be Attacked: Stop Phishing, C2 and Data Exfiltration with Infoblox Threat Intelligence in AWS Network Firewall</a> appeared first on <a href="https://www.infoblox.com/blog">Infoblox Blog</a>.</p>
