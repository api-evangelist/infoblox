---
title: "Hiding in Plain Sight: Abusing Composite Domain Names"
url: "https://www.infoblox.com/blog/security/hiding-in-plain-sight-abusing-composite-domain-names/"
date: "Thu, 09 Apr 2026 16:49:08 +0000"
author: "Vadym Tymchenko"
feed_url: "https://www.infoblox.com/blog/feed/"
---
<p><img alt="" class="attachment-post-thumbnail size-post-thumbnail wp-post-image" height="408" src="https://www.infoblox.com/blog/wp-content/uploads/composite-queries-thumbnail.jpeg" width="612" /></p><h3>Abstract</h3>
<p>Many DNS-based services utilize <strong>composite queries</strong>, which are queries formed by embedding a referenced domain as a subdomain. For example, <span class="code-format">example-com.translate.goog</span> refers to <span class="code-format">example.com</span> as the source domain. The use of composite queries allows services to route users effectively on the Internet; however, these services can also present a security challenge by enabling actors to bypass traditional DNS security controls.</p>
<p>Such services include content proxies (e.g., Google Translate), email security gateways (e.g., Microsoft Outlook Safe Links), content delivery networks, and DNS protocol–based services (such as antivirus lookups and security reputation systems). Malicious actors exploit these mechanisms by passing malicious content through well-known legitimate services, so that the embedded domain is not visited directly from the user’s device, reducing visibility for conventional threat detection systems.</p>
<p>We conducted a comprehensive analysis of services utilizing composite queries in our cloud customer traffic and summarized the purposes and risks they represent. We identified over 100 high-volume services in regular use. Their composite query activity accounts for about 7% of distinct domains, with many embedded domains not visible in direct traffic. Our analysis shows that over 100 known malicious or suspicious domains are embedded in Google Translate queries alone every day.</p>
<p>This blog explains how composite queries are constructed for different purposes and describes how we detect them and accurately extract potentially malicious domains.</p>
<h3>Introduction</h3>
<p>The Domain Name System (DNS) serves as the Internet&#8217;s address book, translating human-readable domain names like www.google.com into IP addresses that computers use to communicate. This fundamental protocol is trusted by network security controls, which attackers may attempt to exploit or bypass.</p>
<p>Domain-embedding services represent a legitimate and widely used class of Internet infrastructure that encodes target domains within DNS query structures. These services create composite DNS queries where the target domain is embedded within the service domain structure, resulting in queries like:</p>
<p><span class="code-format">example-com.translate.goog</span></p>
<p><span class="code-format">subdomain.example.com.cdn-service.net</span></p>
<p><span class="code-format">ZXhhbXBsZS5jb20.proxy-service.example</span></p>
<p>While domain-embedding services serve legitimate purposes—such as translation, email security, content delivery, and privacy protection—they can present security challenges when misused by malicious actors.</p>
<h3>The Security Blind Spot</h3>
<p>Consider a malicious actor attempting to run a phishing campaign from malicious-domain.com. Under normal circumstances, this domain could be:</p>
<ul class="list-spacing">
<li>Blocked by protective DNS systems based on threat intelligence</li>
<li>Flagged by IP reputation systems when connections are established</li>
<li>Identified through SSL certificate analysis</li>
<li>Detected by network security monitoring tools</li>
</ul>
<p>However, when the same malicious domain is accessed through a domain-embedding service as malicious&#8211;domain-com.translate.goog, the security landscape changes:</p>
<ul class="list-spacing">
<li><strong>DNS firewalls</strong> observe queries to translate.goog (Google&#8217;s trusted domain) rather than malicious-domain.com</li>
<li><strong>IP reputation systems</strong> see connections to Google&#8217;s infrastructure (highly trusted) rather than malicious hosting providers</li>
<li><strong>SSL inspection</strong> encounters Google&#8217;s valid certificates rather than suspicious or self-signed certificates</li>
<li><strong>Traditional threat detection</strong> fails because all observable indicators point to legitimate, trusted services</li>
</ul>
<p><img src="https://www.infoblox.com/blog/wp-content/uploads/hiding-in-plain-sight-abusing-composite-domain-names-figure1.jpg" /></p>
<p class="image-caption">Figure 1. An example of a real-world phishing email containing a Google translate link with an embedded malicious website.</p>
<p>This creates a security gap: <strong>the embedded domain can bypass traditional DNS-based security controls</strong> because the observable DNS traffic, IP addresses, and SSL certificates all belong to the legitimate service domain, not the actual embedded destination. These embedded domains reach client systems through various channels—shared links in emails, messaging applications, web pages, and other content—yet remain hidden from security controls focused on the observable service domain.</p>
<h3>Addressing the Gap: A Paradigm Shift in DNS Security</h3>
<p><strong>The detection system shifts the security paradigm from &#8220;trust the observable DNS domain&#8221; to &#8220;extract and analyze the embedded destination.&#8221;</strong> Rather than accepting the service domain at face value, the system:</p>
<ol class="list-spacing">
<li><strong>Identifies domain-embedding services</strong> through analysis of DNS traffic patterns</li>
<li><strong>Extracts embedded domains</strong> using multiple decoding techniques</li>
<li><strong>Validates extracted domains</strong> through statistical conformity analysis against legitimate domain baselines</li>
<li><strong>Applies independent security analysis</strong> to embedded domains using threat intelligence, reputation feeds, and behavioral analysis</li>
<li><strong>Enables granular policy enforcement</strong> where security decisions are based on embedded domain reputation and detected service specialization rather than service domain reputation</li>
</ol>
<p>This paradigm transforms the security response from binary service-level decisions (&#8220;block all translate.goog&#8221; or &#8220;allow all translate.goog&#8221;) to context-aware, content-based policies (&#8220;allow translate.goog when embedding legitimate domains; block or alert when embedding known malicious domains&#8221;). Security response decisions—whether to block all queries to a service, block individual queries associated with known malicious embedded content, or allow traffic—should be made on a case-by-case basis to avoid disrupting critical security and functional services.</p>
<h3>Service Categories and Detection Characteristics</h3>
<p><strong>Service Categories</strong></p>
<p>Observed generic domain-embedding services fall into several categories organized by abuse potential and security risk. Each category has distinct security implications while sharing common DNS traffic patterns that enable automated detection:</p>
<table>
<tr>
<td><strong>Category</strong></td>
<td><strong>Abuse Risk</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td><strong>Content Proxy</strong></td>
<td><strong>High</strong></td>
<td>Services that deliver content of the embedded domain, either direct or transformed. This includes translation services, anonymizers, link wrappers, and web archives that fetch and serve content through their infrastructure. Enables malicious actors to hide domains within trusted infrastructure for phishing and malware delivery.<br />
<strong>Examples:</strong> Google Translate (translate.goog), Microsoft Outlook SafeLinks (protection.outlook.com), web archive services.</td>
</tr>
<tr>
<td><strong>DNS Proxy</strong></td>
<td><strong>High</strong></td>
<td>Services that provide DNS resolution access to embedded domains, returning DNS records for those domains via CNAME records or recursive forwarding. Enables DNS-based hiding of malicious domains.<br />
<strong>Examples:</strong> Public DNS resolvers with embedded query patterns, CNAME-based redirection services for click tracking and campaign management</td>
</tr>
<tr>
<td><strong>Metadata Services</strong></td>
<td><strong>Low</strong></td>
<td>Services that return information <em>about</em> embedded domains (i.e. reputation scores, threat classifications, or status indicators), rather than delivering the domain&#8217;s content itself. These services provide critical security and operational intelligence and should not be blocked.<br />
<strong>Examples:</strong> SURBL (surbl.org), URIBL (uribl.com), antivirus lookup services, reputation systems, domain availability checkers.</td>
</tr>
<tr>
<td><strong>Static Content</strong></td>
<td><strong>Medium</strong></td>
<td>Domains with wildcard DNS records that return identical or non-specific content regardless of subdomain structure. While queries may appear to contain embedded domains, no actual domain-specific embedding occurs. Requires investigation to distinguish legitimate wildcard services from selective abuse where attackers use CNAME records for targeted domains.<br />
<strong>Examples:</strong> CDN wildcards, domain parking pages, anti-caching mechanisms with random prefixes.</td>
</tr>
<tr>
<td colspan="3">Table 1: Categories of domain-embedding services organized by abuse risk and security implications</td>
</tr>
</table>
<p><strong>Common DNS Traffic Characteristics</strong></p>
<p>Despite their diverse purposes and risk profiles, services across all categories share observable DNS traffic patterns that enable automated detection:</p>
<p><strong>Subdomain Structure Patterns</strong>:</p>
<ul class="list-spacing">
<li><strong>High subdomain diversity</strong>: Services generate hundreds to thousands of unique subdomains as they handle different embedded destinations</li>
<li><strong>Structural consistency</strong>: Repeated patterns (prefixes, suffixes) appear across all queries to the same service</li>
<li><strong>Encoding consistency</strong>: Each service uses a consistent encoding approach</li>
</ul>
<p><strong>DNS Query Characteristics</strong>:</p>
<p>DNS query characteristics vary between detected services. These characteristics are useful for attribution of services to categories and understanding associated risks:</p>
<ul class="list-spacing">
<li><strong>Query type distribution</strong>: The distribution of query types (A, AAAA, CNAME, TXT, etc.) provides insights into service function</li>
<li><strong>Infrastructure patterns</strong>: Resolution targets and their stability over time</li>
<li><strong>ASN and hosting analysis</strong>: Concentration or distribution of infrastructure across autonomous systems</li>
<li><strong>Provider reputation</strong>: Assessment of hosting infrastructure providers</li>
</ul>
<p><strong>Volume and Temporal Patterns</strong>:</p>
<ul class="list-spacing">
<li><strong>Sustained activity</strong>: Legitimate services show consistent query volumes over time</li>
<li><strong>Multiple embedded destinations</strong>: True domain-embedding services handle diverse target domains, not just single-organization subdomains</li>
<li><strong>Temporal stability</strong>: Service infrastructure and patterns remain stable across observation periods</li>
</ul>
<p>Table 2 shows representative examples of direct DNS traffic compared to domain-embedding service traffic patterns across different risk categories:</p>
<table>
<tr>
<td><strong>Category</strong></td>
<td><strong>Example Service</strong></td>
<td><strong>Query Pattern</strong></td>
<td><strong>Pattern Description</strong></td>
</tr>
<tr>
<td>Direct Traffic</td>
<td>N/A</td>
<td>google.com</td>
<td>Standard domain query</td>
</tr>
<tr>
<td>Direct Traffic</td>
<td>N/A</td>
<td>mail.example.com</td>
<td>Typical subdomain/ hostname structure</td>
</tr>
<tr>
<td><strong>Content Proxy (High Risk)</strong></td>
<td>Google Translate</td>
<td>example-com.translate.goog</td>
<td>Embedded encoded domain</td>
</tr>
<tr>
<td><strong>DNS Proxy (High Risk)</strong></td>
<td>CDN Service</td>
<td>example.com.cdn-provider.net -&gt; example.com</td>
<td>Direct subdomain embedding with CNAME</td>
</tr>
<tr>
<td><strong>Metadata Services (Low Risk)</strong></td>
<td>Antivirus Lookup</td>
<td>mfrggzdfmztwq2lk.av-service.net</td>
<td>Encoded domain for threat intelligence lookup</td>
</tr>
<tr>
<td colspan="4">Table 2: DNS query patterns showing direct traffic vs. domain-embedding service traffic</td>
</tr>
</table>
<h3>Methodology: Multi-Stage Detection Pipeline</h3>
<p>The detection system operates as a multi-stage pipeline, with each stage building upon the previous one, progressively refining and enriching detections of domain-embedding services.</p>
<p><strong>Stage 1: Service Domain Detection</strong></p>
<p>The first stage identifies service domain candidates by analyzing domains with abnormally high subdomain diversity. For each candidate, the system attempts to decode embedded domains using multiple decoding techniques and detects consistent structural patterns.</p>
<p>To validate decoded domains, the system builds statistical baselines from direct DNS traffic, capturing domain name properties. Decoded domains are scored against this baseline, allowing it to filter out random strings and other composite components.</p>
<p>Candidates are classified by confidence level based on the number of validated embedded domains, destination diversity, encoding consistency, and statistical conformity scores.</p>
<p><strong>Stage 2: Enrichment and Validation</strong></p>
<p>Detected service domains and embedded domains are enriched with external intelligence: domain registration data, historical DNS observations, reputation feeds, SSL certificates, and others. External sources such as WHOIS and historical DNS records confirm that embedded domains are legitimate registered domains rather than random artifacts. Validation filters ensure temporal consistency, encoding consistency, destination diversity, and registration data coverage to reduce false positives.</p>
<p><strong>Stage 3: Aggregation and Trend Analysis</strong></p>
<p>The final stage aggregates validated detections across time periods to track service domain lifecycles, identify growing or declining services, and maintain historical context on domain-embedding service evolution.</p>
<h3>Results: Discovery and Analysis of DNS Traffic Blind Spots</h3>
<p>The detection system reveals significant gaps in traditional DNS security monitoring and provides insights into domain-embedding service usage patterns.</p>
<p><strong>Discovery of Previously Unobserved Traffic</strong></p>
<p>Analysis of DNS traffic demonstrates the substantial blind spot created by composite queries:</p>
<p><strong>Composite Query Volume</strong>: Queries to domain-embedding services produce a sizable portion of DNS traffic, with their composite query patterns representing a measurable fraction of total query volume. This traffic typically bypasses traditional security analysis focused on direct domain queries.</p>
<p><strong>Unique Domain Discovery</strong>: Activity associated with embedded domains represents approximately <strong>7% of distinct domain activity in daily traffic</strong>. This includes over 10,000 domains per day that are not queried directly at our cloud DNS resolvers. A notable portion of these embedded domains are not observed in direct traffic within extended observation periods.</p>
<p><strong>Service Domain Identification</strong>: The system identified approximately 100 domain-embedding services daily, categorized across multiple confidence levels based on embedding patterns, destination diversity, and encoding consistency.</p>
<p><img src="https://www.infoblox.com/blog/wp-content/uploads/hiding-in-plain-sight-abusing-composite-domain-names-figure2.jpg" /></p>
<p class="image-caption">Figure 2. Daily activity of domains using composite queries</p>
<p><strong>Service Distribution</strong>: Analysis of domain-embedding traffic over a two-week period reveals significant concentration among a small number of services. Microsoft Outlook SafeLinks (outlook.com) dominates the landscape at 71.7% of observed traffic, followed by Google Translate (5.3%), Cloudflare (2.7%), URIBL (0.74%), and SURBL (0.45%). The remaining 19.1% is distributed across about a hundred smaller services. This distribution pattern remains consistent across all sampling periods, validating the stability of our observations. Figure 3 shows this distribution.</p>
<p><img src="https://www.infoblox.com/blog/wp-content/uploads/hiding-in-plain-sight-abusing-composite-domain-names-figure3.jpg" /></p>
<p class="image-caption">Figure 3. Distribution of embedded traffic between services</p>
<p><strong>Embedded Domain Characteristics</strong></p>
<p><strong>Domain Age Distribution</strong>: Analysis reveals a notable presence of newly registered domains among embedded domains. On average, approximately 100 unique domains per day were registered within the past 7 days, and approximately 350 unique domains per day were registered within the past 30 days.</p>
<p><img src="https://www.infoblox.com/blog/wp-content/uploads/hiding-in-plain-sight-abusing-composite-domain-names-figure4.jpg" /></p>
<p class="image-caption">Figure 4. Domains registered within past 7 days (30 days) window</p>
<p><strong>Service-Specific Analysis</strong></p>
<p>Detailed analysis of 3 well-known domain-embedding services demonstrates diverse usage patterns and risk profiles, illustrating different security considerations from open proxies to critical security infrastructure:</p>
<p><strong>Google Translate (translate.goog) &#8211; Content Proxy</strong></p>
<p>Among the highest-volume services detected, they process thousands of unique embedded domains daily. Approximately 10,000 unique embedded domains are observed daily, with 6.6% not present in direct DNS traffic on the same day. Queries resolve Google&#8217;s infrastructure, fetching and serving content through trusted infrastructure. 0.3% of embedded domains matched threat intelligence feeds (phishing sites, malware distribution, suspicious recently-registered domains)—representing tens to hundreds of malicious domains daily that bypass traditional security controls. While legitimate use cases represent the majority, even a small number of successful attacks can compromise organizations.</p>
<p><strong>SURBL (multi.surbl.org) &#8211; DNS Protocol-Based Service</strong></p>
<p>Email security gateways and spam filters generate moderate query volumes to this threat intelligence service. Analysis observed approximately 1,000 unique embedded domains, with 6.5% not appearing in direct DNS traffic. Rather than resolving embedded domains, SURBL returns encoded threat classifications as pseudo-IP addresses in the 127.0.0.x range. As essential security infrastructure, SURBL enables real-time threat assessment—60% of queried embedded domains represent known malicious or suspicious threats. This service should not be blocked, as it is critical to security operations.</p>
<p><strong>Microsoft Outlook SafeLinks (protection.outlook.com) &#8211; Email Security Gateway</strong></p>
<p>Very high volume in enterprise environments reflect widespread Microsoft 365 adoption. Approximately 250,000 unique embedded domains were observed, with 0.4% not present in direct DNS traffic on the same day. Queries resolve Microsoft&#8217;s protection infrastructure, scanning embedded URLs before redirecting users. 0.2% of embedded domains match threat intelligence feeds—over a thousand malicious or suspicious domains daily. While this represents a lower malicious rate compared to open proxies like Google Translate, the absolute volume demonstrates that significant malicious activity reaches users through this trusted channel. This service is an example of a valid infrastructure that should not be interrupted, but embedded domains represent valuable contributions to threat analysis.</p>
<h3>Conclusion</h3>
<p>Modern DNS security requires looking beyond observable domains. Our research reveals that thousands of domains daily remain hidden within trusted infrastructure, invisible to traditional security tools focused on direct DNS queries.</p>
<p>Infoblox&#8217;s detection system provides visibility into this previously hidden activity. By extracting embedded domains from composite queries and applying independent threat analysis, security teams can now identify and respond to threats regardless of how attackers attempt to obscure them—while preserving the functionality of legitimate services that organizations depend on.</p>
<p>This capability represents a significant advancement in DNS security. Organizations gain comprehensive visibility across both direct and embedded domain activity, enabling context-aware policies that protect users without disrupting business operations. As domain-embedding services continue to grow in usage, this visibility becomes increasingly essential for maintaining effective security postures.</p>

<p><span class="gradient"></span></p>
		<div class="wpulike wpulike-default "><div class="wp_ulike_general_class wp_ulike_is_restricted"><button class="wp_ulike_btn wp_ulike_put_image wp_post_btn_13296" type="button"></button><span class="count-box wp_ulike_counter_up"></span>			</div></div>
	<p>The post <a href="https://www.infoblox.com/blog/security/hiding-in-plain-sight-abusing-composite-domain-names/">Hiding in Plain Sight: Abusing Composite Domain Names</a> appeared first on <a href="https://www.infoblox.com/blog">Infoblox Blog</a>.</p>
