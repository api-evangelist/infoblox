---
title: "Hold the Phone! International Revenue Share Fraud Driven by Fake CAPTCHAs"
url: "https://www.infoblox.com/blog/threat-intelligence/hold-the-phone-international-revenue-share-fraud-driven-by-fake-captchas/"
date: "Thu, 23 Apr 2026 12:55:49 +0000"
author: "Infoblox Threat Intel"
feed_url: "https://www.infoblox.com/blog/feed/"
---
<p><img alt="" class="attachment-post-thumbnail size-post-thumbnail wp-post-image" height="408" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-thumbnail.jpeg" width="612" /></p><p><strong>Authors: David Brunsdon, Darby Wise</strong></p>
<h3>Executive Summary</h3>
<p>CAPTCHAs, the mundane tasks where we demonstrate our ability to select bicycles or distinguish chihuahuas from blueberry muffins, are increasingly being weaponized to trick users into performing actions with unexpected consequences. Fake CAPTCHAs are commonly associated with ClickFix attacks but have also been leveraged in other kinds of campaigns, including those we&#8217;ve documented in our blog on <a href="https://www.infoblox.com/blog/threat-intelligence/inside-a-malicious-push-network-what-57m-logs-taught-us/">malicious push notifications</a>. One way we&#8217;ve observed fake CAPTCHA pages used in campaigns is related to a telecommunications fraud scheme known as international revenue share fraud (IRSF).</p>
<p><img alt="Image" class="blog-image" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-image1-5.png" /></p>
<p>Over a year ago, we encountered a website employing an unusual technique for distinguishing humans from bot traffic: it required us to send SMS messages to proceed. Only more recently did we realize how these underreported scams work. When the user follows the instructions, the messages are sent internationally and result in charges on the victim&#8217;s phone bill, with a share of that revenue going to the actor who leases the phone numbers and operates the fake CAPTCHA site.</p>
<p>Digging further, we found that this operation has existed since at least June 2020 and uses several tricks to ensnare victims, such as socially engineered lures and back button hijacking. During our research, we observed the use of 35 phone numbers spanning 17 countries, including those known to have high termination fees, such as Azerbaijan, Egypt, and Myanmar.</p>
<p>The fake CAPTCHA has multiple steps, and each message crafted by the site is preconfigured with over a dozen phone numbers, meaning the victim isn&#8217;t charged for just a single message—they&#8217;re charged for sending SMSs to over <strong>50 international destinations</strong>. This type of scam also benefits from delayed billing, as the &#8216;international SMS&#8217; charges often appear on the victim&#8217;s bill weeks later and the experience with the fake CAPTCHA has been long forgotten. In our experience, the process generated 60 SMS messages, which could cost a user $30; these are small amounts individually, but they could quickly add up for the threat actor.</p>
<p>Our investigation revealed a sophisticated, multi-stage fraud operation that demonstrates the convergence of two critical threats: IRSF and malicious traffic distribution systems (TDSs). While telecom companies have long understood IRSF as a significant source of revenue loss, this research shows that TDS infrastructure, the same systems that direct users to scareware or malware, also funnels victims into SMS scams at scale. The TDS infrastructure enables precise victim targeting while obscuring the malicious landing pages from security researchers and automated detection systems.</p>
<p>The campaigns also incorporate back button hijacking, wherein a site interferes with the browser’s history and prevents users from returning to a previous &#8220;safe” site when they hit the back button. Google <a href="https://developers.google.com/search/blog/2026/04/back-button-hijacking" target="_blank">recently announced a ban</a> on the use of the technique, calling it a malicious practice.</p>
<p>This operation defrauds both individuals and telecommunication carriers simultaneously. Individual victims face unexpected premium SMS charges on their bills and would have difficulty identifying and reporting the fraud when it originates from such an unexpected source. Telecom carriers pay revenue share to the perpetrators while likely absorbing the losses from customer disputes or chargebacks. The TDS-driven distribution across multiple countries and phone numbers makes it nearly impossible for an individual carrier to see the full scope of the fraud affecting themselves and their customers, thereby allowing the operation to persist undetected across a fragmented regulatory landscape.</p>
<p>And so, unfortunately, it needs to be said: Do not send a text to confirm you are human.</p>
<h3>On International Revenue Share Fraud</h3>
<p>IRSF is a <a href="https://www.akamai.com/blog/security/understanding-international-revenue-share-fraud" target="_blank">telecommunications fraud scheme</a> where criminals exploit the international call and SMS termination fee system to generate fraudulent revenue. When you send an international SMS, your carrier pays a termination fee to the destination country&#8217;s carrier to complete the connection, with rates that can cost pennies or much more, depending on the receiving country. In IRSF schemes, fraudsters register phone numbers in countries with high termination fees or lax regulations, like Azerbaijan, Kazakhstan, or certain premium-rate number ranges in Europe; and establish revenue-sharing agreements with local telecom providers.</p>
<p>When victims are tricked into calling or sending SMS messages to these numbers, the fraudster receives a portion of the termination fee. IRSF is one of the most lucrative and persistent forms of telecom fraud globally. According to FTI Consulting&#8217;s 2025 <a href="https://contents.comms.delinian.com/rs/462-OQR-635/images/GLF%20Fraud%20Report%202025.pdf?version=0" target="_blank">Global Fraud Loss Report</a> for the Global Leaders Forum, artificially inflated traffic (AIT), which includes traffic generated through IRSF schemes, is the most financially damaging type of messaging fraud, with 50% of telecommunications carriers reporting high financial losses and 54% reporting high traffic volumes. With global fraud losses that are measured in billions annually, IRSF is a big deal.</p>
<p>When encountering this scheme, the user will see a fake CAPTCHA and be prompted several times, with different CAPTCHA images, to send SMS messages. Figure 1 shows a partial sequence recorded on our research device in February 2025, and video of a full “user experience” is <a href="https://youtu.be/CMxO_ChUVkc" target="_blank">here</a>.</p>
<div class="grid-container">
<div class="grid-item">
<img alt="Figure 1a" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure1a.png" />
</div>
<div class="grid-item">
<img alt="Figure 1b" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure1b.png" />
</div>
</div>
<div class="grid-container">
<div class="grid-item">
<img alt="Figure 1c" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure1c.png" />
</div>
<div class="grid-item">
<img alt="Figure 1d" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure1d.png" />
</div>
</div>
<p class="image-caption">Figure 1. When a user encounters this IRSF actor, they will be taken through a series of fake CAPTCHAs, each requiring an SMS message to prove they are human. The images demonstrate a partial sequence of this experience. Source: Infoblox Threat Intel.</p>
<h3>Traversing the TDS</h3>
<p>When confronted with a fake CAPTCHA page, you might ask yourself, ‘How did I get here?’. The answer is, quite likely, a traffic distribution system (TDS). <em>Our regular readers will think: of course!</em></p>
<p>In March 2026, we triggered this threat by visiting a lookalike domain to a major U.S. telecom company. From the lookalike domain, we were immediately redirected into a TDS (via <span class="code-format">colnsdital[.]com</span>) and were then passed to <span class="code-format">hotnow[.]sweeffg[.]online</span>, which we attribute with a high degree of confidence to a commercial TDS that is part of an affiliate advertising network based in Germany. From there, we were redirected to another TDS node, this one controlled by our SMS scam actor: <span class="code-format">zawsterris[.]com</span>. In other words, the SMS scam actor is an advertising affiliate of the commercial TDS operator. We have not studied this affiliate network in-depth, and we do not know if they are aware of the affiliates using their network for this kind of fraud.</p>
<p>The next redirection was to the fake CAPTCHA page: <span class="code-format">d[.]ruelomamuy[.]com</span>. After completing the CAPTCHA process, the TDS sent us to <span class="code-format">megaplaylive[.]com</span>, another actor-controlled domain hosting gaming and video content that seems benign on the surface but is capable of continuing the scam. This redirect chain is shown in Figure 2, with the final three steps in red showing domains controlled by this SMS actor.</p>
<p><img alt="Figure 2" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure2.png" /></p>
<p class="image-caption">Figure 2. Initial observed redirection chain leading to fake a CAPTCHA page hosted on d[.]ruelomamuy[.]com</p>
<p>Several observations allowed us to associate the TDS node <span class="code-format">zawsterris[.]com</span> to the SMS scam actor. The most notable one came through DNS: before hiding behind Cloudflare, <span class="code-format">zawsterris[.]com</span> briefly resolved to an IP on AS15699 (Adam Ecotech), which is the same infrastructure we&#8217;d already linked to this SMS fraud campaign. Table 1 shows hosting and registration information for the domains used in this redirection chain.</p>
<table>
<tr>
<td><strong>Domain</strong></td>
<td><strong>Function</strong></td>
<td><strong>IP ISP</strong></td>
<td><strong>Registrar</strong></td>
<td><strong>Attribution</strong></td>
</tr>
<tr>
<td>&lt;telecom typosquat&gt;</td>
<td>Entry point</td>
<td>Digital Ocean</td>
<td>Media Elite</td>
<td>Unknown</td>
</tr>
<tr>
<td><span class="code-format">colnsdital[.]com</span></td>
<td>TDS node</td>
<td>Hetzner</td>
<td>Namesilo</td>
<td>Unknown</td>
</tr>
<tr>
<td><span class="code-format">hotnow[.]sweeffg[.]online</span></td>
<td>TDS node</td>
<td>Internap</td>
<td>GoDaddy</td>
<td>Commercial affiliate advertising network</td>
</tr>
<tr>
<td><span class="code-format">zawsterris[.]com</span></td>
<td>TDS node</td>
<td>Cloudflare</td>
<td>GoDaddy</td>
<td>SMS scam actor</td>
</tr>
<tr>
<td><span class="code-format">d[.]ruelomamuy[.]com</span></td>
<td>Landing Page</td>
<td>Cloudflare</td>
<td>GoDaddy</td>
<td>SMS scam actor</td>
</tr>
<tr>
<td><span class="code-format">megaplaylive[.]com</span></td>
<td>Landing Page</td>
<td>Adam Ecotech</td>
<td>GoDaddy</td>
<td>SMS scam actor</td>
</tr>
<tr>
<td colspan="5">Table 1. Domains used in the redirection chain</td>
</tr>
</table>
<p>To monetize traffic in a TDS, tracking information needs to be passed along, and these details are typically put into the URL. Table 2 shows the parameters we observed during the commercial TDS stage of the redirection change, and Table 3 shows the parameters observed during the SMS scam portion.</p>
<table>
<tr>
<td><strong>Campaign Parameter</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td>utm_medium</td>
<td>aa3e8d3009d94b9c89ac744b2be0687643493b0c</td>
</tr>
<tr>
<td>utm_campaign</td>
<td>sweeffg</td>
</tr>
<tr>
<td colspan="2">Table 2. Commercial affiliate advertising network campaign parameters</td>
</tr>
</table>
<table>
<tr>
<td><strong>SMS Scam Parameter</strong></td>
<td><strong>Value</strong></td>
</tr>
<tr>
<td>clientId</td>
<td>254</td>
</tr>
<tr>
<td>productId</td>
<td>2001</td>
</tr>
<tr>
<td>publisher_id</td>
<td>23188&amp;MU1FFF</td>
</tr>
<tr>
<td>af</td>
<td>5002320649344840</td>
</tr>
<tr>
<td>groupds</td>
<td>166</td>
</tr>
<tr>
<td colspan="2">Table 3. SMS scam campaign parameters</td>
</tr>
</table>
<p>The <strong>productId</strong> parameter was particularly interesting, as the value of <strong>2001</strong> appears both here and in the cookie analysis as a value in the list of “valid_products.” It implies that this landing page is one among many, and the campaign is much larger in scope than what we have observed.</p>
<h3>Technical Overview</h3>
<p>The fake CAPTCHA&#8217;s mechanics are straightforward but deceptive. It leverages social engineering by mimicking familiar verification tasks such as animal identification and text recognition, while hiding a crucial requirement: users must send an SMS message to proceed. This design funnels traffic to phone numbers distributed across 17 countries.</p>
<p>The CAPTCHA’s level of difficulty seems intentionally trivial. The fraud doesn&#8217;t depend on challenge complexity; it depends on SMS volume. Each of the multi-stage verification steps triggers a separate message to the server-designated numbers. The codebase handles both iOS and Android platforms through sophisticated server-side control, orchestrating each user action via command-and-control (C2) infrastructure. At a high level, the operation is as follows:</p>
<ol class="list-spacing">
<li>User clicks any answer to a fake CAPTCHA question</li>
<li>JavaScript calls <span class="code-format">makeTrackerDownload.php</span> API endpoint</li>
<li>Server returns phone numbers, SMS message, and control parameters</li>
<li>JavaScript launches SMS app with pre-filled message and phone numbers</li>
<li>After 5 seconds, JavaScript decides next action based on server instructions</li>
</ol>
<p>When the victim submits an answer to the fake CAPTCHA, their phone launches their messaging app with a preconfigured message and destinations comprising the entire list of phone numbers. The user would then just have to hit send. With four steps of CAPTCHA, and 15 numbers identified in this attempt, <strong>60 SMS messages in total are sent</strong>, maximizing the actor’s revenue across multiple countries and carriers.</p>
<p>There are four questions in the CAPTCHA process in step 1 above, which include asking for your device type (iOS or Android) and your network (3G, 4G, or WiFi). Each step triggers sending a message via SMS, which is prepopulated with the entire list of phone numbers received from the website. The DOM of the website also reveals the content of messages that are sent. Each message contains an {af}, for affiliate code, which is likely used to track the multiple campaigns that drive traffic to the site, and two contain {respuesta}, which is the answer for the question (“respuesta” is Spanish for response).</p>
<p>From the code:</p>
<ol class="list-spacing">
<li>sms1 = &#8220;I want to continue {af}&#8221;</li>
<li>sms2 = &#8220;The option I choose is {respuesta} {af}&#8221;</li>
<li>sms3 = &#8220;The option I choose is {respuesta} {af}&#8221;</li>
<li>sms4 = &#8220;Im not bot im real user {af}&#8221;</li>
</ol>
<p>The control parameters mentioned in step 2 above allow dynamic updates to the operation to override default behavior. They include:</p>
<ol class="list-spacing">
<li>“forceRedirectURL,” which could function as either a kill-switch or a redirection to drive traffic to another page</li>
<li>“forceMessage,” which allows operators to change the SMS message without updating the HTML; this could be used to adapt to carrier filtering or language localization, among other possibilities</li>
</ol>
<h4>Back Button Hijacking</h4>
<p>In addition to SMS-based social engineering, this campaign employs a dedicated <a href="https://www.adsecure.com/blog/how-to-stop-back-button-hijack" target="_blank">back button hijacking</a> mechanism to trap users on the fake CAPTCHA pages and increase the likelihood of SMS interaction. The dedicated JavaScript (see Figure 3), first observed in this campaign in January 2023, manipulates the user’s browser history using the pushState() method, effectively neutralizing the browser’s back button. When a user attempts to navigate away from the page via the back button, the script pushes the current page URL onto the history stack, logs the action to a server-side endpoint, and redirects the user back to the fake CAPTCHA page. This creates a navigation loop preventing the user from leaving the page without fully exiting the browser.</p>
<p><img alt="Figure 3" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure3.png" /></p>
<p class="image-caption">Figure 3. JavaScript for back button hijacking</p>
<p>Typically, the backlinkURL is the same as the URL the user is already on; however, in some cases, the value of the variable is set to a different URL hosting the same kind of scam page. Figure 4 shows an example for <span class="code-format">d[.]herbosfinx[.]com</span>. If a user in this case were to hit the back button, they would be redirected to a new CAPTCHA hosted on <span class="code-format">d[.]santafebuno[.]top</span>.</p>
<p><img alt="Figure 4" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure4.png" /></p>
<p class="image-caption">Figure 4. Code with backlink and log URL for d[.]herbosfinx[.]com. Source: <a href="https://urlscan.io/result/019991d4-e4bb-773f-917e-0df8a7529e1c" target="_blank"><strong>urlscan.io</strong></a> </p>
<h3>Terms of Service</h3>
<p>The operators of the scam aren’t without their attempts at plausible deniability. At the bottom of the CAPTCHA pages is a form of legal fine print we often see with scams that attempt to deflect responsibility for the operation.</p>
<p><img alt="Figure 5" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-image1-5.png" /></p>
<p class="image-caption">Figure 5. Text at the bottom of the CAPTCHA page</p>
<p>The disclaimer frames the CAPTCHA as a service exchange, then places the burden onto the victim to research pricing of international SMS. It does not state that there will be multiple SMS messages sent to over a dozen international destinations. The costs for the unreasonable number of SMS messages will be extraordinarily high due to the actor’s curation of the most expensive destinations to increase their return. This type of disclaimer is not a disclosure: it’s misdirection from the fact that the entire CAPTCHA process is fake.</p>
<h3>Phone Number Analysis</h3>
<p>The website’s DOM reveals how to retrieve the phone numbers used to drive the scam. Using a GET request observed in the code, we can craft a simple curl command to query the server and retrieve the phone numbers. Additionally, nested in the response is a key, “urlContent,” which contains the destination to redirect the victim to, bundled with a base64 string within the URL. In our example, the decoded string contains 20 additional phone numbers, which after the completion of the CAPTCHA process, were passed within the redirection to the <span class="code-format">megaplaylive[.]com</span> domain.</p>
<h4>Example curl command (safelinked, complete numbers redacted):</h4>
<p><span class="code-format">curl -s &#8216;https://d[.]ruelomamuy[.]com/makeTrackerDownload.php?a=WEBSMS&amp;s=5002320649344849&amp;c=US&amp;groupds=138&amp;caf=5002320649344849&amp;origSms=I%20want%20to%20continue%205002320649344849&amp;step=9&#8217; | jq .</span></p>
<h4>Response (safelinked):</h4>
<p><span class="code-format">{<br />
  &#8220;phoneNumbers&#8221;: &#8220;+9947764824XX;+31970391393XX;+31970391383XX;+4473560342XX;+2652229761XX;+324802180XX;+337576670XX;+417846132XX;+9592636943XX;+316352451XX;+324640995XX;+3937803063XX;+487802079XX;+9051026608XX;+347007503XX&#8221;,<br />
  &#8220;os&#8221;: null,<br />
  &#8220;urlContent&#8221;: &#8220;http://megaplaylive[.]com/?enc=eyJwaG9uZU51bWJlcnMiOlsiKzIwMTAwNTc5NzQ1MiIsIisyMDEwMDQ5MzkxNzgiLCIrMjAxMDA1Nzk2Mzg5IiwiKzIwMTAwNDk1MTYyNiIsIisyMDEwMDU4MDMzNzkiLCIrMjAxMDA2MzQ4ODc5IiwiKzIwMTAwNDkzOTE0NSIsIisyMDEwMDUyMDk2NzYiLCIrMjAxMDA2MzQzOTk3IiwiKzIwMTAwNjM1MzY5MyIsIisyMDEwMDk0MDg1ODQiLCIrMjAxMDA1Nzk2Mzk5IiwiKzM4MDkyNzg4NTQ2MiIsIiszODA5MjI0MTg0MDQiLCIrNDQ3NDkwOTIwODEwIiwiKzQ2NzY2NzQ2NDUxIiwiKzQzNjcwMzA2ODEwNyIsIis3NzkwNTAwMDIyNSIsIiszMjQ2NzQ0MDQyNyIsIis0NDc4NDg1MDk0NDgiXSwiYWYiOiI1MDAyMzIwNjQ5MzQ0ODQ5IiwiZGV2IjpudWxsLCJ0eXBlIjoiZ2FtZXMiLCJsYW5nIjoiZW4iLCJsb2FkZXIiOmZhbHNlLCJjaWQiOm51bGwsInBpZCI6bnVsbH0=&#8221;,<br />
  &#8220;codeAF&#8221;: &#8220;lfzmfSzw&#8221;<br />
}</span></p>
<p>From these commands we have two tiers of phone number lists. One is used in the CAPTCHA scheme (see Table 4), and the other is passed onwards to the ‘game’ site <span class="code-format">megaplaylive[.]com</span> (Table 5).</p>
<p>The phone numbers illustrate a global range of SMS destinations, spanning seventeen countries, including many locations known for having higher than average termination fees, such as the Netherlands, Myanmar, and Azerbaijan.</p>
<h4>15 Tier 1 Phone Numbers (from a single fake CAPTCHA)</h4>
<table>
<tr>
<td><strong>Number</strong></td>
<td><strong>Country</strong></td>
<td><strong>Code</strong></td>
</tr>
<tr>
<td>9947764824XX</td>
<td>Azerbaijan</td>
<td>+994</td>
</tr>
<tr>
<td>31970391393XX</td>
<td>Netherlands</td>
<td>+31</td>
</tr>
<tr>
<td>31970391383XX</td>
<td>Netherlands</td>
<td>+31</td>
</tr>
<tr>
<td>4473560342XX</td>
<td>UK</td>
<td>+44</td>
</tr>
<tr>
<td>2652229761XX</td>
<td>Malawi</td>
<td>+265</td>
</tr>
<tr>
<td>324802180XX</td>
<td>Belgium</td>
<td>+32</td>
</tr>
<tr>
<td>337576670XX</td>
<td>France</td>
<td>+33</td>
</tr>
<tr>
<td>417846132XX</td>
<td>Switzerland</td>
<td>+41</td>
</tr>
<tr>
<td>9592636943XX</td>
<td>Myanmar</td>
<td>+95</td>
</tr>
<tr>
<td>316352451XX</td>
<td>Netherlands</td>
<td>+31</td>
</tr>
<tr>
<td>324640995XX</td>
<td>Belgium</td>
<td>+32</td>
</tr>
<tr>
<td>3937803063XX</td>
<td>Italy</td>
<td>+39</td>
</tr>
<tr>
<td>487802079XX</td>
<td>Poland</td>
<td>+48</td>
</tr>
<tr>
<td>9051026608XX</td>
<td>Turkey</td>
<td>+90</td>
</tr>
<tr>
<td>347007503XX</td>
<td>Spain</td>
<td>+34</td>
</tr>
<tr>
<td colspan="3">Table 4. List of phone numbers used in CAPTCHA scheme</td>
</tr>
</table>
<h4>20 Tier 2 Phone Numbers (passed to <span class="code-format">megaplaylive[.]com</span>)</h4>
<table>
<tr>
<td><strong>Number</strong></td>
<td><strong>Country</strong></td>
<td><strong>Code</strong></td>
</tr>
<tr>
<td>2010057974XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010049391XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010057963XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010049516XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010058033XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010063488XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010049391XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010052096XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010063439XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010063536XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010094085XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>2010057963XX</td>
<td>Egypt</td>
<td>+20</td>
</tr>
<tr>
<td>3809278854XX</td>
<td>Ukraine</td>
<td>+380</td>
</tr>
<tr>
<td>3809224184XX</td>
<td>Ukraine</td>
<td>+380</td>
</tr>
<tr>
<td>4474909208XX</td>
<td>UK</td>
<td>+44</td>
</tr>
<tr>
<td>467667464XX</td>
<td>Sweden</td>
<td>+46</td>
</tr>
<tr>
<td>4367030681XX</td>
<td>Austria</td>
<td>+43</td>
</tr>
<tr>
<td>779050002XX</td>
<td>Kazakhstan</td>
<td>+7</td>
</tr>
<tr>
<td>324674404XX</td>
<td>Belgium</td>
<td>+32</td>
</tr>
<tr>
<td>4478485094XX</td>
<td>UK</td>
<td>+44</td>
</tr>
<tr>
<td colspan="3">Table 5. Phone numbers used passed to game site</td>
</tr>
</table>
<p>After completing the fake CAPTCHA, the victim is redirected to <span class="code-format">megaplaylive[.]com</span>, which seems to only exist for the purpose of this operation, and like many of the domains mentioned in this article, is hosted on AS15699 (Adam EcoTech). As demonstrated with URLScan, the <a href="https://urlscan.io/result/019d01e7-275f-7628-a491-dcf15282e92f/" target="_blank">page cannot be accessed directly</a> by visiting the second-level domain (SLD) <span class="code-format">megaplaylive[.]com</span>. We observed an example of the fake CAPTCHA process leading to <span class="code-format">megaplaylive[.]com</span> on the <a href="https://app.any.run/tasks/03bf3208-4d46-4b9c-858b-d07eff62653f" target="_blank">online sandbox tool ANY.RUN.</a></p>
<p>It wasn’t until we researched the domain thoroughly that we uncovered the ‘contentType’ parameter, which when set to ‘sexy’ revealed the continuation of the SMS scam. With the correct settings, we could access a page where the code demonstrated how each click of ‘play’ on an adult video would launch another SMS message configured with 20 international recipients. The ‘sexy’ (their word) version of megaplaylive loads <a href="https://urlscan.io/result/019d02cc-f1bc-726a-a0ef-fd966a8f9fd0/dom/" target="_blank">JavaScript</a> that controls this portion of the operation.</p>
<h3>DNS Patterns</h3>
<p>The actor hosts the fake CAPTCHA pages in this campaign on both SLDs and various subdomains of these SLDs. SLDs can vary but most follow one of two patterns shown in Table 6. Subdomains include <span class="code-format">cd</span>, <span class="code-format">chat</span>, <span class="code-format">click</span>, <span class="code-format">d</span>, <span class="code-format">r</span>, <span class="code-format">raffles</span>, <span class="code-format">v</span>, <span class="code-format">vids</span>, etc., with <span class="code-format">d</span> and <span class="code-format">r</span> used most frequently.</p>
<table>
<tr>
<td><strong>Domain Pattern</strong></td>
<td><strong>Examples</strong></td>
</tr>
<tr>
<td>RDGA-generated domains featuring repeated words/strings (typically used in two or three domains) mixed with other random words or characters</td>
<td>panzo<strong>zerrot</strong>[.]com / <strong>zerrot</strong>mamil[.]com<br />
  remotes<strong>buffalo</strong>[.]top / <strong>buffalo</strong>solpe[.]top<br />
  vister<strong>transit</strong>[.]com / <strong>transit</strong>caxip[.]com<br />
  fufe<strong>carrol</strong>[.]top / <strong>carrol</strong>vassin[.]top</td>
</tr>
<tr>
<td>Domains/subdomains featuring content themes, e.g., win, chat, tips, vids.</td>
<td><span class="code-format">vids[.]chatorizon[.]com</span><br />
  <span class="code-format">chat[.]matchnewtoday[.]com</span><br />
  <span class="code-format">claimandwins[.]com</span><br />
  <span class="code-format">4lifetips[.]com</span></td>
</tr>
<tr>
<td colspan="2">Table 6. Domain patterns used in CAPTCHA campaign</td>
</tr>
</table>
<p>DNS analysis shows most domains and subdomains used in this campaign have consistently resolved to a small set of dedicated IP addresses on an ASN based in Spain (AS15699 Adam EcoTech, S.A.) since the first observed CAPTCHA page in June 2020.</p>
<p>Domains are registered using NameSilo or GoDaddy and use DNS Made Easy (DME) and DigiCert nameservers. Some domains following the web content theme (chat, tips, giveaway, etc.) have been seen using dedicated name servers.</p>
<p>During this investigation, we repeatedly observed references to an affiliate advertising network based in Europe. We have not studied this company in-depth, and we do not know if they are aware of the use of their network for IRSF fraud. The company’s website claims they are “the greatest company for Click2SMS” and that they offer carrier billing with “all kinds of traffic allowed.” Click2SMS is an affiliate marketing model that generates revenue through carrier billing by prompting mobile users to send an SMS message to a designated number(s) through a single click. Based on the name servers and other technical supporting information, we are confident that the threat actor we observed is an affiliate of this Click2SMS network.</p>
<p>Mentions of the company name and Click2SMS can be seen in website code, in registration and hosting information for some of the domains, and even in dedicated cookies these domains use for tracking. The company’s origins are also similar to many other elements in this campaign, including the language of the code, as well as the IP space used to host the CAPTCHA pages and the nameservers of the gaming/adult content domains.</p>
<p>The company was referenced in the <span class="code-format">megaplaylive[.]com</span> website code related to the push notification service it employs. For years, Infoblox Threat Intel has reported on cases where actors use push notifications to establish persistence on a victim’s device, and that is again likely the case here. If a victim were to allow push notifications, the operator of the service would gain the ability to drive notifications to the device, directing the victim to return to the site for new content, or send them elsewhere to other scams.</p>
<h3>Cookie Analysis</h3>
<p>Similar to other adtech and TDS operations, this campaign relies heavily on browser cookies to track user and campaign attributes, as well as dynamically control traffic flow. These cookies store contextual information such as user geolocation, language, internet service provider (ISP), etc. Additional cookie values track progression through the multi-stage verification flow, enforce step limits, and even set a rate of probable success of the campaign, allowing operators to filter non-optimal users. The fake CAPTCHA pages have set the same three to four seemingly dedicated tracking cookies since the beginning of this campaign in June 2020, including cookies mentioning tracking and <span class="code-format">c2s</span>, likely referring to Click2SMS. Table 7 below shows an example of one of the decoded cookie values.</p>
<div style="border: 1px solid; margin-bottom: 20px;">
<div style="margin: 20px;">
<span class="code-format">{“isp”:”&lt;redacted&gt;”,usa”,”country”:”US”,”lang”:”en”,”clientId”:”248″,”operator”:”&lt;redacted&gt;”,”action”:null,”valid_products”:[1414,1415,1416,1417,1418,1422,2841,2842,2843,1732,1896,1897,2822,2823,2834,1898,1899,1904,2563,1870,1981,1831,1814,2791,2798,2793,2800,2661,2666,1907,2665,2670,2790,2797,2845,2664,2669,2663,2668,2794,2801,2792,2799,1676,2795,2802,2796,2803,1829,1815,2662,2667,1847,1722,1738,1749,1748,1874,1843,1724,1827,1718,1872,1913,1970,2807,2812,2805,2810,2804,2809,1717,2024,2806,2811,2816,2808,2813,1727,2838,1909,1825,1750,2562,1849,1721,1863,1747,1853,1720,1971,1768,1767,1857,1855,2774,1902,2829,2828,1697,1763,1839,1764,1845,1723,2839,1968,1972,1769,1716,1728,2781,1726,1725,1835,1711,1851,1719,1841,1741,2780,1911,2001,1861,1859,1837,1733,1715,1900,1766,2833,1823,1821,2840,1765,1964,1963,1890,1889,1892,1891,1680,1967,1966,2509,2508,1868,2510,2513,1866,1975,2511,2514,2512,2515,1710,2771,2772,2773,2827,2824,2826,2825,1713,1714,1983,1969,1988,2071,1658,1657,1977,1591,1592,1593,1594,1595,1596,1974,1997,1752,1411,1706,1701,1665,1405,1404,1406,1503,1502,1504,1505,1908,1943,1942,1702,1547,1635,1627,1628,1629,1630,1631,1632,1633,1675,1941,1940,1906,2609,1616,1744,1705,1672,1667,2072,1699,1673,1599,1481,2250,1651,1662,1650,1654,1656,1655,1647,1648,1649,1660,1663,2028,1668,1666,1408,1407,1409,2023,1597,1659,1559,2070,1598,1536,1540,1652,1653,1901,1987,1637,1674,1537,1538,1539,1961,1413,1420,1421,1412,1499,1679,1696,1483,1661,1579,1484,1570,1553,1581,1490,1546,1580,1485,1550,1569,1486,1541,1712,1833,1803,1482,1636,1487,1551,1556,1568,1535,1488,1554,1552,1555,1489,1340,1460,1366,1367,1368,1341,1342,1449,1450,1451,1369,1370,1371,1372,1373,1425,1423,1424,1343,1344,1345,1354,1617,1626,1618,1619,1620,1621,1622,1623,1624,1625,1664,2002],”invalid_product”:null,”successRate”:0}</span></p>
<p style="border-top: 1px solid black; padding-top: 10px; margin-top: 10px;">Table 7. Decoded cookie value set by <span class="code-format">d[.]marraheltin[.]com</span></p>
</div>
</div>
<p>We observed the success rate value stored in the cookie value being actively used by the fake CAPTCHA page’s client‑side code to determine the user’s next action based on their suitability for the campaign, as shown in Figure 6.</p>
<p><img alt="Figure 6" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure6.png" /></p>
<p class="image-caption">Figure 6. Code used to redirect non-targeted users to other fake CAPTCHA pages</p>
<p>When the user is on the first step of the CAPTCHA flow, the code evaluates a pre-calculated successRate value stored in the cookie containing data on the user. If the user is deemed a non-ideal candidate for the campaign, the page redirects them to an alternate URL defined by the externOffer variable, which points to a new fake CAPTCHA page. The differences in hosting and registration patterns of the SLDs set in the externOffer variables, along with stylistic differences in the CAPTCHA pages, indicate these may be part of a separate campaign or controlled by a different actor. Figure 7 shows an example of these new pages impersonating Lush, a legitimate cosmetics company (don’t miss the time-pressure tactic: don’t let robots claim the bath bomb—complete the form!). The externOffer value for this page is set to:</p>
<p><span class="code-format">hXXps://verifysuper[.]com/cl/i/wopmej?aff_sub4=5002320649344849&amp;aff_sub5=US</span></p>
<p><img alt="Figure 7" src="https://www.infoblox.com/blog/wp-content/uploads/fake-captcha-figure7.png" /></p>
<p class="image-caption">Figure 7. externOffer fake CAPTCHA page impersonating Lush Cosmetics and hosted on verifysuper[.]com.  Source: <a href="https://urlscan.io/result/019ce93d-286c-7498-853a-519b7cfc2361/" target="_blank"><strong>urlscan.io</strong></a></p>
<h3>SMS: Another Drop in the Scam Bucket</h3>
<p>This research represents one operation we were able to thoroughly document; however, the history of the domains, the application of affiliate codes, and international telecom and TDS infrastructure suggest that it is not unique, but rather part of a broader ecosystem. Visiting a typosquat domain of a major telecom brand is what originally initiated this investigation, and that led us to an international revenue sharing fraud scheme that seems to have gone underreported for years—one that creates victims of both individuals and telecoms. Our findings here add to our years of research showing that the malicious use of TDSs is one of the most significant threats on the internet today, and brings attention to a new lesson: avoiding pop-ups, spoofed pages, and compromised sites isn’t enough to stay safe: don’t send texts to confirm you are human either.</p>
<h3>Indicators</h3>
<p>A curated selection of indicators related to the threats discussed can be seen in the table below. A more comprehensive list of indicators can be found in our <a href="https://github.com/infobloxopen/threat-intelligence" target="_blank">GitHub repository</a>.</p>
<p><em>Note: Some domains/hostnames listed below may no longer be active or used in this campaign.</em></p>
<table>
<tr>
<td><strong>Indicators</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td><span class="code-format">colnsdital[.]com</span></td>
<td>TDS domain leading to fake CAPTCHA page</td>
</tr>
<tr>
<td><span class="code-format">hotnow[.]sweeffg[.]online</span></td>
<td>Commercial TDS hostname</td>
</tr>
<tr>
<td><span class="code-format">zawsterris[.]com</span></td>
<td>SMS-actor controlled TDS domain</td>
</tr>
<tr>
<td><span class="code-format">megaplaylive[.]com</span><br /><span class="code-format">chat[.]matchnewtoday[.]com</span><br /><span class="code-format">vids[.]chatorizon[.]com</span></td>
<td>SMS actor-controlled domains hosting fake gaming, chat, and video content</td>
</tr>
<tr>
<td><span class="code-format">d[.]fufecarrol[.]top</span><br /><span class="code-format">d[.]herbosfinx[.]com</span><br /><span class="code-format">d[.]marraheltin[.]com</span><br /><span class="code-format">d[.]panzozerrot[.]com</span><br /><span class="code-format">d[.]remotesbuffalo[.]top</span><br /><span class="code-format">d[.]ruelomamuy[.]com</span><br /><span class="code-format">d[.]santafebuno[.]top</span><br /><span class="code-format">d[.]vistertransit[.]com</span><br /><span class="code-format">d[.]zerrotmamil[.]com</span><br /><span class="code-format">r[.]buffalosolpe[.]top</span><br /><span class="code-format">r[.]carrolvassin[.]top</span><br /><span class="code-format">r[.]transitcaxip[.]com</span></td>
<td>SMS actor-controlled domains actively hosting fake CAPTCHA pages</td>
</tr>
<tr>
<td><span class="code-format">claimandwins[.]com 4lifetips[.]com</span></td>
<td>Domains hosting older versions of the fake CAPTCHA/download pages</td>
</tr>
<tr>
<td><span class="code-format">verifysuper[.]com</span></td>
<td>externOffer domain hosting fake CAPTCHA pages</td>
</tr>
</table>

<p><span class="gradient"></span></p>
		<div class="wpulike wpulike-default "><div class="wp_ulike_general_class wp_ulike_is_restricted"><button class="wp_ulike_btn wp_ulike_put_image wp_post_btn_13360" type="button"></button><span class="count-box wp_ulike_counter_up"></span>			</div></div>
	<p>The post <a href="https://www.infoblox.com/blog/threat-intelligence/hold-the-phone-international-revenue-share-fraud-driven-by-fake-captchas/">Hold the Phone! International Revenue Share Fraud Driven by Fake CAPTCHAs</a> appeared first on <a href="https://www.infoblox.com/blog">Infoblox Blog</a>.</p>
