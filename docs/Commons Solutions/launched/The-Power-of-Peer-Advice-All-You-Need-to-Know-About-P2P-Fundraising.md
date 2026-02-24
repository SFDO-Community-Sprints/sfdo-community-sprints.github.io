---
title: The Power of Peer Advice - All You Need to Know About P2P Fundraising
nav_order: 1
parent: Launched Solutions
---

# The Power of Peer Advice: All You Need to Know About P2P Fundraising

**What Is Peer to Peer Fundraising?**

Peer to Peer (P2P) fundraising is a strategy where a nonprofit empowers its supporters to raise money on its behalf, rather than the organization doing all the asking itself. Instead of the organization asking for every donation directly, supporters create personal fundraising pages and solicit donations from friends, family, colleagues, and social connections. This approach expands the organization's reach beyond its existing donor base, leveraging trusted relationships to inspire giving. P2P fundraising is often used for events like walks, runs, and challenges, but it can also include digital campaigns and milestone-based fundraisers. At its core, P2P fundraising turns passionate supporters into advocates, storytellers, and ambassadors, multiplying impact through community-driven engagement.

---

**What Is the Difference Between Traditional P2P & DIY Fundraising?**

**Traditional P2P Fundraising**

Traditional Peer to Peer (P2P) Fundraising is an organization-led fundraising campaign where individuals (and often teams) raise money on behalf of an organization as part of a structured event or initiative. These are typically time-bound and centrally managed by the nonprofit.

**Examples**

* Walks, runs, and rides
* Golf tournaments
* Ambassador programs
* Workplace/team fundraising challenges

**Key Characteristics**

* Organization sets the date, goal, branding, and messaging
* Fundraisers register for a specific campaign/event
* Often includes teams and corporate sponsors
* Typically tied to an in-person or hybrid event
* Clear start/end date
* Registration fees may apply

**What You (May) Need to Track in Salesforce**

* Fundraiser (Individual) vs Donor (Individual)
* Team Captain vs Participant
* Offline gifts credited to fundraiser
* Registration fees vs Donations
* Matching gifts
* Corporate team revenue rollups

**DIY Fundraising**

Do It Yourself (DIY) fundraisers are traditionally created independently by an individual for a personal reason or milestone, usually without being attached to a structured event.

**Examples**

* Birthdays
* Memorial/tribute pages
* Athletic challenges (outside of an organized event)
* Personal milestones (wedding, retirement, new baby)

**Key Characteristics**

* Supporter-driven (not event-driven)
* Often evergreen or loosely time-bound
* Usually no registration fee
* Minimal organizational oversight
* Highly personal storytelling
* Can happen year-round

---

**P2P Fundraising: NPSP & AFNP Considerations**

When designing a P2P solution in Salesforce, it's important to understand how the underlying data model differs between Nonprofit Success Pack (NPSP) and Agentforce Nonprofit (AFNP). While both can support sophisticated P2P programs, the way objects relate to one another, and how fundraising activity is structured, impacts your integration design, automation strategy, and reporting framework.

In NPSP, P2P fundraising typically relies heavily on standard objects such as Campaigns, Campaign Members, Contacts, Accounts (Households), and Opportunities, with soft credits used to attribute revenue to fundraisers. More complex P2P programs often require additional customization, including custom objects (if not provided by your P2P platform connector), roll-up summaries for fundraiser and team totals, custom reporting logic, and automation for goal tracking. Campaign hierarchy plays a central role, particularly when structuring year-specific events.

In AFNP, the model shifts toward a more modern architecture that separates fundraising concepts more explicitly (e.g. gift transactions, commitments, designations), and may leverage Data Cloud for high-volume or complex event data. AFNP environments often rely more heavily on automation (Flow), structured program design, and integrated marketing journeys to manage participant onboarding, milestone tracking, and stewardship at scale.

Regardless of model, a strong P2P implementation starts by reverse-engineering your reporting and engagement requirements. You'll need to determine the minimum data required to:

* Create or match a Contact/Person Account record for each fundraiser
* Assign them to the appropriate year-specific P2P Campaign
* Soft credit all gifts to the responsible fundraiser
* Trigger onboarding and milestone journeys (often via Marketing Cloud or other marketing tools, with Data Cloud recommended for complex participant tracking)
* Build dashboards that track both overall campaign performance and individual fundraiser progress

Understanding how NPSP or AFNP structures these relationships ensures your data flows cleanly from your fundraising platform into Salesforce and, more importantly, supports long-term reporting, recognition, and retention strategies. It is important to reverse engineer minimum data collection from the perspective of reporting requirements and future use to contact the fundraisers to acknowledge and encourage participation for future events.

**NPSP Data Model**

|**Object**|**Purpose in P2P**|
|  ---  |  ---  |
|**Account**|The Household of the donor or fundraiser.|
|**Contact**|Individual donor or fundraiser.|
|**Opportunity**|The actual cash donation ($250).|
|**Campaign**|Links the donation to the specific P2P Event or Page.|
|**Soft Credit**|**Crucial:** Credits the fundraiser for the money they "raised" without counting it as their personal tax-deductible gift.|

**AFNP Data Model**

|**Object**|**Purpose in P2P**|
|  ---  |  ---  |
|**Person Account**|Represents the individual (No more separate Contact/Account sync).|
|**Gift Transaction**|The financial record of the gift.|
|**Gift Commitment**|Used if the P2P donor sets up a recurring gift.|
|**Campaign**|Still used for source tracking.|
|**Outreach Source**|A new object in AFNP to track exactly which link or page drove the gift.|

---

**How Campaigns Can Support Your Fundraising**

In Salesforce, the Campaign object is the backbone of a P2P and DIY fundraising data model because it's the cleanest way to organize fundraising activity, attribute revenue, and report consistently over time. Whether you're running a traditional P2P event (like a run/walk) or supporter-led DIY fundraising (like a birthday or tribute page), Campaigns give you a shared structure to tie together the key pieces: who participated (Campaign Members), who donated (Contacts/Accounts), and what was raised. When integrations are configured well, Campaigns also make it far easier to answer the questions teams care about most: revenue by event, by fundraiser, by cohort, and year-over-year trends.

In the architecture community there is a constant discussion as to how Campaign hierarchies should be structured for P2P and DIY fundraising. In Salesforce there is a native requirement to maintain a Campaign hierarchy structure with a maximum of 5 levels within the hierarchy. Thus, it is imperative to be strategic about the way you use your hierarchy levels. For example, it can be tempting to create an "ultimate parent" Campaign like "Run Event - All Time" and nest each year underneath it so you can see the lifetime of giving in a single record. In practice, that top-level roll-up isn't always necessary, if you are thoughtful on how to run reporting in an efficient manner. 

If you already create a Campaign record for each instance of an event, for example, "Run 2025," "Run 2026," "Run 2027", you can often get the same cross-year reporting by adding a simple classification field (e.g. Event Series = Run, Event Type = P2P Run/Walk, Region, Fiscal Year) and filtering/grouping reports on those fields. This approach keeps the Campaign hierarchy cleaner, reduces admin overhead, and avoids forcing every event into a single "forever" parent structure, while still giving you easy "all time" reporting when you need it.

Before selecting tools or beginning any technical configuration, the first step in designing a successful P2P solution should be defining and mapping your Campaign hierarchy strategy. Clearly defining how you want to structure events, DIY efforts, teams, years, and reporting rollups will shape everything that follows, from integrations to automation to executive dashboards. It's equally important to confirm how your chosen fundraising platform supports (or constrains) that structure, particularly around campaign creation, hierarchy sync, attribution, and roll-up reporting. We strongly recommend researching and aligning on this campaign framework *before* technical implementation begins. Thoughtful planning at this stage prevents rework later, ensures clean reporting from day one, and creates a scalable foundation as your P2P and DIY programs grow.

**Typical Campaign Structure**

* Parent Campaign (The Event): E.g. "Annual Walkathon 2026".
* Child Campaign (Team Level): E.g. "Marketing Team Walkers".
* Grandchild Campaign (Individual Fundraiser Page): E.g. "Sarah's  Fundraising Page".

**Campaign Hierarchy: Traditional P2P Fundraising**

Typically modelled in Salesforce as:

* Parent Campaign (e.g. 2026 Walk for Hope)
* Child Campaigns:
    * Teams
    * Individual Fundraisers
* Contacts/Accounts (Person) = Participants
* Opportunities/Gift Transactions = Donations
* Campaign Members = Registrants / Fundraisers

You often need:

* Team hierarchy tracking
* Registration status
* Fundraiser goal tracking
* Event attendance tracking
* Corporate team affiliation
* Sponsorship tracking

**Campaign Hierarchy: DIY Fundraising**

Typically modelled as:

* One Campaign per DIY fundraiser *or*
* One umbrella "DIY Fundraising" campaign with individual tracking via:
    * Custom fields (DIY Type = Birthday, Memorial, etc.)
    * Sub-campaigns per page

---

**Integration Options**

**AMER**

In the North American (AMER) market, a handful of fundraising platforms consistently rise to the top for organizations running P2P and DIY campaigns. While there are many tools available, the platforms outlined below represent some of the most commonly adopted solutions among U.S. and Canadian nonprofits, particularly those looking to scale events, supporter-led fundraising, and digital giving while integrating with Salesforce. Each brings a slightly different strength to the table, from enterprise-grade event management to conversion-optimized donation experiences.

|**Platform**|**Overview**|**Considerations**|**Integration**|
|  ---  |  ---  |  ---  |  ---  |
|[**DonorDrive**](https://www.donordrive.com/)|DonorDrive is an enterprise-grade Peer to Peer fundraising and event platform designed to help nonprofits create rich, engaging fundraising experiences (walks, runs, hybrid virtual events, DIY pages, livestream fundraisers, teams, leaderboards, etc.). It emphasizes supporter engagement through coaching tools, social sharing, gamification, and flexible event configuration.<br>Highlights:<br>* Robust P2P + DIY support (personal pages, teams, event management) <br>* Mobile app experience for fundraisers and donors <br>* Built-in engagement tools (love meters, gamification, social sharing) <br>* Scalable for large nonprofit and higher-ed portfolios|* Typically positioned at the enterprise level, meaning pricing and implementation effort may be higher than lightweight tools. <br>* Smaller nonprofits with simple needs may find it more than they need or costly. <br>* Feature depth can lead to a steeper setup curve (though strong support and training are available).|DonorDrive offers an [**AppExchange integration**](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000DqCoPUAV) that syncs key fundraising data including donors, events, supporters, teams, and donations into Salesforce. Mapping and integration configuration are **_customizable_**, and it leverages Salesforce native features like matching and duplicate management. <br>* Salesforce records (Contacts/Accounts, Campaigns, Opportunities) can be populated.<br>* Field mapping and syncing logic can be tailored.<br>* Sync covers event participation, tickets, campaign tags, and fundraising activity. <br>* Supports both NPSP and AFNP data models.|
|**[Go Fund Me Pro ](https://pro.gofundme.com/)(formerly Classy)**|Classy, now part of GoFundMe Pro, is a widely used online fundraising platform built specifically for nonprofits with strong P2P, crowdfunding, and event fundraising features. It supports branded fundraising pages, campaign customization, recurring gifts, and participant engagement tools.<br>Highlights:<br>* Strong toolset for campaign pages and supporter journeys. <br>* Versatile for both traditional P2P events and DIY campaigns. <br>* Good donor experience and branding options.|* Some organizations find customization and reporting require deeper platform familiarity.<br>* Some organizations have reported that the integration can be 'buggy' and fail at times.<br>* In depth knowledge of the Contact matching solution Go Fund Me Pro has is required.<br>* Implementation and support can require time and coordination.|GoFundMe Pro has a robust Salesforce integration, [**available via AppExchange**](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N30000000pv6PEAQ), that provides near-real-time sync of donors, transactions, campaigns, and related engagement data into Salesforce.<br>* Data flows into appropriate Salesforce objects with deduplication and matching. <br>* Supports event details and registrations synced as related records (attendees, orders). <br>* Historical data sync may need support team intervention for backfills. <br>* Supports both NPSP and AFNP data models.|
|[**OneCause**](https://www.onecause.com/)|OneCause is a versatile fundraising platform focused on P2P events, auctions, ticketed events, and online giving. It offers tools that help nonprofits combine events with digital fundraising, gamification, social sharing, and ticket/registration management. <br>Highlights:<br>* End-to-end support for P2P campaigns, registrations, and fundraising pages. <br>* Additional event tools (auctions, bidding, ticketing, text-to-give). <br>* Built-in supporter engagement tools (social integration, dashboards).|* Customization complexity may require planning for mapping and data governance.<br>* Reporting depth depends on how you structure your pages and event data.|OneCause provides a Salesforce integration, most commonly with the Salesforce Nonprofit Success Pack (NPSP). It uses automatic or scheduled syncs to push supporter, giving, and event information into Salesforce objects (Contacts, Accounts, Opportunities, Activities). <br>* Sync can run daily or on demand. <br>* Some data may be stored in OneCause-branded custom objects linked to Salesforce standards.<br>* Offers configuration for how fields map and how records match/overwrite. <br>* Setup is typically managed by a Salesforce admin, and sandbox testing is recommended.<br>* Offers custom API for complex integrations<br>* Now available for both NPSP and AFNP.|
|[**Fundraise Up**](https://fundraiseup.com/)|Fundraise Up is a digital fundraising platform focused primarily on maximizing online giving conversion through AI-driven optimization, making donation forms easy to complete and increasing revenue. It supports robust donation pages, donor portals, email receipts, and payment flexibility (including global currencies).<br>Highlights:<br>* High-conversion donation pages using AI optimization. <br>* Seamless donor checkout + support for many payment methods. <br>* Strong analytics and insights dashboard. |* **Not primarily built for full P2P event management:** while supporters can raise funds via personalized donation pages, it lacks the deep event, team, and registration features that classic P2P platforms offer. This functionality is on the product roadmap (as of February 2026).<br>* DIY use cases (e.g. birthday fundraisers) can be supported through personalized pages, but you may need custom flows if you want deeper campaign hierarchy management.|Fundraise Up does not have a widely advertised native AppExchange connector, however they do offer a FundraiseUp built connector that can be configured via your FundraiseUp instance.|

**Honourable Mentions**

Below are some honourable mentions - additional platforms that aren't as universally adopted in AMER P2P or DIY fundraising, but still worth considering depending on your organization's needs, audience, or technical strategy. These tools may excel in specific use cases like hybrid event support, flexible campaign models, cost, or integrated constituent engagement, and can be strong complements or alternatives to the core platforms outlined above.

* [Springboard](https://www.jacksonriver.com/springboard)
* [Give Lively](https://www.givelively.org/)
* [GiveButter](https://givebutter.com/?_gl=1*8ta4zr*_up*MQ..*_gs*MQ..&gclid=CjwKCAiAkvDMBhBMEiwAnUA9BY8jHDJ1sKFVUlNghFziq4rZD3CQdyxFUizy0mri_pPw1Oq50m6IMhoCCp0QAvD_BwE&gbraid=0AAAAApeSZX0H6liXQDgqk-9IM9jADnSzm)
* [Zeffy](https://www.zeffy.com/)
* [DonorBox](https://donorbox.org/)
* [Funraise](https://www.funraise.org/)

**APAC**

Across the APAC region, the P2P and DIY fundraising landscape reflects a mix of globally recognized platforms and strong regional providers. Many organizations in Australia and New Zealand, in particular, rely on purpose-built P2P event technology that supports large-scale participation campaigns, while others prioritize flexible digital tools that enable year-round supporter-led fundraising. The platforms highlighted below represent some of the most commonly used solutions across APAC nonprofits, especially for organizations looking to balance event fundraising, DIY campaigns, and Salesforce integration needs.

|**Platform**|**Overview**|**Considerations**|**Integration**|
|  ---  |  ---  |  ---  |  ---  |
|[**Raisely**](https://www.raisely.com/)|Raisely is a online fundraising platform designed specifically for nonprofits, charities, and social enterprises. <br>* Out of the box features<br>* A solution for the APAC region. <br>* Allows organizations to create, manage, and scale digital fundraising campaigns. Such as: donation appeals, P2P and event registration without needing technical or coding expertise. <br>* Support big campaigns <br>* Need Stripe/Paypal payment gateways.|* **Online Appeals:** Running urgent or specific, time-bound fundraising appeals.<br>* **Peer-to-Peer Campaigns:** Challenges, DIY fundraising, or virtual events.<br>* **Regular Giving:** Tools designed to convert one-time donors into monthly supporters.<br>* **Event Ticketing:** Handling registrations and tickets for events.|**Native Pro**<br>* Raisely built integration, can map data to CRM, self managed.<br>**Zapier**<br>* Self managed, DIY cheapest option.<br>**MoveData**<br>* Available in the app exchange, data mapping robust, managed by the org.|
|[**Grassrootz**](https://www.grassrootz.com/platform)|Grassrootz an online fundraising platform for charities in Australia and New Zealand, specializing in P2P campaigns, community event fundraising, and custom donation pages. <br>Enables nonprofits to create, manage, and scale fundraising efforts, often integrating directly with major sporting events like marathons to drive donations. |* **Peer-to-Peer Fundraising:** Supporters create personal, customizable fundraising pages linked to a charity's campaign, such as charity runs or memorial fundraising.<br>* **Major Community Events:** Charities connect with large, organized events (e.g., City2Surf, Melbourne Marathon) to manage official, branded, and peer-to-peer fundraising.<br>* **Ticketing & Registration:** An all-in-one flow allows participants to register for events, purchase merchandise, join teams, and start fundraising in a single transaction.<br>* **Targeted Campaigns:** Creating specialized pages for appeals, including "in-memory" fundraising, virtual campaigns, and tax-time, donation-driven appeals|* MoveData/Zapier<br>* No native integration|
|[**Funraisin**](https://www.funraisin.co/)|2026, Funraisin stands as a premium, global digital fundraising platform tailored for nonprofits that want total control over their brand and data. <br>Founded in 2014 in Sydney, Australia, it has grown into an "enterprise-grade" solution used by over 1,000 charities worldwide, including UNICEF, Cure Cancer, and The Hunger Project.|### Advanced Peer-to-Peer (P2P) & DIY<br>It manages massive events (like the *Distinguished Gentleman's Ride*) by providing:<br>* **Gamification:** Automated badges, leaderboards, and milestones.<br>* **Fitness Integration:** Native sync with Strava, Fitbit, Garmin, and MapMyFitness.<br>* **Virtual Missions:** Ability to map real-world fitness data to virtual routes (e.g., "Walking across the Sahara").<br>### Branding & Content Management (CMS)<br>Funraisin is often used as a charity's entire website, not just a donation page.<br>* **Visual Builder:** A drag-and-drop editor that allows non-tech staff to build high-converting landing pages.<br>* **White-Labeling:** Full control over CSS and HTML, ensuring the site is "pixel-perfect" and mobile-responsive.<br>### Integrated eCommerce & Ticketing<br>It replaces secondary tools like Eventbrite or Shopify by including:<br>* **Ticketing:** Management of registrations, "waves" for fun runs, and VIP tiers.<br>* **Merchandise:** A built-in shop for selling t-shirts, water bottles, or virtual gifts (e.g., "Buy a goat for a village").<br>### Data-First Marketing<br>Because it isn't a third-party portal, the data it generates is incredibly deep:<br>* **Marketing Automation:** Native "Nudge" triggers (SMS/Email) based on fundraiser behavior.<br>* **Deep Analytics:** Full visibility into ROI by tracking exactly which social media ad led to a specific donation.|* Native integration, rich data mapping|

**Honourable Mentions**

In addition to the leading platforms, there are several other solutions gaining traction across APAC that may be a strong fit depending on your campaign model, internal resources, or regional footprint. These honourable mentions often shine in niche areas, such as digital-first fundraising, lightweight DIY campaigns, or localized event support, and can be effective options for organizations with specific operational or budget considerations.

* [GiveNow](https://www.givenow.com.au/)
* [JustGiving](https://www.justgiving.com/)

**EMEA**

To be built at a future sprint - please add in! :slightly_smiling_face:

---

**Guidance for Nonprofits - Our Recommendations & Advice**

**Leveraging Your P2P Data for Marketing**

To provide a consistent, personalized, and well-governed experience for supporters, it is recommended that all fundraising-related emails are sent via a single communications channel. The recommendations below assume the use of **Marketing Cloud**, connected.

**Why use Marketing Cloud as the single email channel?**

**1. Improves supporter experience**

Sending emails from one platform ensures communications feel coordinated, timely, and professional.

Key benefits include:

* Greater ability to personalize and brand emails using Salesforce data
* Avoidance of outdated templates or incorrect branding
* Consistent sender details and messaging tone across all communications
* Reduced risk of supporters being over-emailed or confused by messages from multiple systems

**2. Reduces operational risk**

Centralizing email delivery simplifies governance and lowers the risk of errors. This enables the organization to:

* Manage communication preferences and opt-outs in one place for all emails
* Reduce the likelihood of duplicate or conflicting sends
* Maintain clearer ownership and oversight of supporter communications

**3. Increases confidence in data and reporting**

Using a single channel provides a more complete and trustworthy view of communications.

This includes:

* A 360-degree view of all emails sent to donors and fundraisers
* Visibility either directly in Marketing Cloud or written back as records in Salesforce
* Stronger confidence in reporting and analysis of engagement and outcomes

**When Marketing Cloud Emails Can be Triggered**

Marketing Cloud communications can be triggered at multiple points throughout the P2P or DIY fundraising journey.

**For fundraisers:**

* On registration
* When a donation is made to their fundraiser
* When a fundraising milestone is reached (e.g. 50% of goal achieved)

**For donors:**

* On donation

**Data Requirements to support Marketing Cloud Emails**

Marketing Cloud is connected to Salesforce either directly or via Data Cloud. To enable email sending, the required data must be captured and available in Salesforce.

**Information required for fundraisers:**

* Fundraiser name
* Fundraiser email address
* Fundraiser campaign
* Relevant email opt-in indicator
* Fundraising goal
* Funds raised (both individual donation amounts and total raised to date)

**Information required for donors:**

* Donor name
* Donor email address
* Relevant email opt-in indicator
* Fundraising campaign
* Donation amount
* Donation date

---

**Reporting Needs**

A well-designed P2P or DIY fundraising solution is only as strong as the reporting that supports it. Clear, reliable reporting allows organizations to measure performance, understand supporter behaviour, and make informed decisions about future campaigns. Before building integrations or configuring campaign structures, it's important to identify the core questions your organization needs to answer, whether that's total event revenue, fundraiser performance, donor acquisition, retention trends, or year-over-year growth. The sample reports outlined below represent common reporting requirements for peer-to-peer and DIY fundraising programs and can serve as a practical starting point when designing your Salesforce data model and campaign hierarchy.

* Traditional P2P Reporting Needs
    * Total event revenue
    * Revenue by team
    * Revenue by fundraiser
    * Average raised per participant
    * Registration conversion rate
    * Fundraiser retention year-over-year
    * Corporate team performance
* DIY Reporting Needs
    * Revenue by DIY type (Birthday vs Memorial)
    * Top DIY fundraisers
    * First-time donor acquisition via DIY
    * Conversion of DIY fundraisers into:
        * Recurring donors
        * Event participants
        * Major gift prospects

---

**Common Customization Needs**

Beyond data structure and reporting, P2P and DIY fundraising programs often require thoughtful automation and customization within Salesforce to fully support the supporter journey. While your fundraising platform may handle front-end experiences like page creation and donation processing, Salesforce plays a critical role in structuring data, campaign analysis, stewardship, and long-term retention strategies. The common customization needs outlined below reflect the types of automations and other configuration some organizations frequently build to create a seamless and scalable fundraising experience.

* **Salesforce Platform**
    * **Auto-stamping Parent Campaign ID**
        * When a child Campaign (e.g. Team or Individual Fundraiser Campaign) is created, automatically associate it to the correct Parent Event Campaign.
    * **Auto-populating Event Series or Event Type fields**
        * Example: If Campaign Name contains "Run 2026," stamp Event Series = Annual Run.
    * **Automatic Campaign Member status updates**
        * When someone registers, update status to "Registered."
        * After event date, update to "Attended" or "No Show." - depending on whether attendance tracking is required.
    * **Ensuring Opportunities inherit correct Campaign attribution**
        * Especially important when donations come through integrated platforms.
    * **Building Custom Rollups**
        * Roll-up summaries or Flow-based calculations
            * Total Raised by Fundraiser
            * Total Raised by Team
            * Offline gifts credited to participant
        * Progress-to-goal calculations
            * Percentage of fundraising goal achieved
        * Team Captain identification logic
            * Custom fields or roles to identify leadership
    * **Registration & Revenue Handling**
        * Separating registration fees vs. tax-deductible gifts
        * Handling ticket purchases (if applicable)
        * Mapping order line items to Opportunities correctly (depending on the selected tool)
        * Managing refunds or transfers
        * Assigning soft credits to fundraisers
    * **Cross Year Tracking**
        * Participant Year-over-Year flags
        * "First Time Participant" vs "Returning Participant" fields
        * Lifetime P2P revenue reporting
        * Event series classification fields (instead of using an ultimate parent Campaign)
* **Business Process Enablement: Traditional P2P Fundraising**
    * Registration confirmation (sometimes on the platform of your choice)
    * Fundraiser coaching emails
    * Milestone nudges ("You're 75% to goal!")
    * Post-event retention messaging
    * Lapsed participant reactivation next year
* **Business Process Enablement: DIY Fundraising**
    * Annual reminder workflow - automation to encourage your fundraiser to participate again (e.g. sign up again for your birthday)
    * Memorial anniversary touchpoint
    * Personalized thank-you recognizing milestone

---
