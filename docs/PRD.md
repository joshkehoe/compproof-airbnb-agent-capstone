# Product requirements: My capstone prototype

These are the learner's saved capstone answers, in the order they were asked, up to the point where building starts. Each one is a decision the learner accepted. Build what they describe. Where an answer leaves something open, choose the simplest thing that fits and say what you chose.

## Discovery

### 1. Specific user

**Question:** Who is the specific user this agent helps?

I am the initial user: an Airbnb property owner and host who manages the property as a side business. I need help analyzing competing listings and expert-informed market data so I can make better decisions about pricing, occupancy, revenue, and whether potential property upgrades or investments are likely to generate a worthwhile ROI. My constraints are limited time and limited firsthand market-analysis expertise, so I need outputs that are practical and decision-ready rather than generic advice. This capstone focuses on my own property and decisions; making the system available to other Airbnb hosts is a future stretch goal.

### 2. Recurring workflow

**Question:** What recurring workflow are you improving? Write the current workflow in plain text.

I periodically review my Airbnb listing against nearby competing listings to decide how to improve its competitiveness. Today, I would need to manually find and compare competitor titles, descriptions, amenities, prices, photos, and sometimes reviews, then combine that research with advice from trusted short-term-rental experts. Based on that work, I decide what listing-content change to prioritize—for example, replacing or adding a photo, rewriting a description line, or adding or removing an amenity. I expect to revisit this analysis monthly, with the option to run it more often during the July–September high season; however, for this five-week capstone I will validate the workflow with a one-time dataset of 10–15 nearby comps and my own listing rather than build a live refresh pipeline. Pricing is a related decision, but I already use PriceLabs for pricing automation, and physical property upgrades such as buying furniture are secondary future use cases. The MVP focuses on producing evidence-backed, reviewable recommendations for the single best listing-content improvement to make first.

### 3. Workflow trigger

**Question:** What event starts the workflow?

The workflow starts with an initial competitive-analysis run for this capstone. After that, I intend to trigger it on the first day of each month because competing Airbnb listings and market conditions change over time. During the July–September high season, I would run it every Sunday so I can reassess my listing more frequently. For this capstone, I will demonstrate one run using a fixed dataset rather than build the live scheduled refresh pipeline.

### 4. Current process steps

**Question:** List the current process as numbered text steps. Do not link to a process map.

1. I log in to PriceLabs and review its competitive pricing and occupancy analysis for my Airbnb listing.
2. I use PriceLabs to identify competing properties within three miles of my property that appear to outperform my listing.
3. I open the Airbnb pages for approximately 5–15 of those competing listings, usually in separate browser tabs.
4. I manually compare each competitor with my own listing, reviewing photos, title and description content, amenities, price, listing settings, and sometimes guest reviews.
5. I note perceived gaps between my listing and the stronger competitors, such as photo quality or order, missing amenities, weaker listing copy, or settings such as minimum-stay restrictions.
6. I watch trusted short-term-rental experts on YouTube to validate which gaps are likely to matter most and decide what to prioritize.
7. I choose an action. For the core listing-content workflow, this may mean changing photo order, adding or replacing a photo, rewriting description content, or adding or removing an amenity. In some cases, I also consider a capital upgrade, such as adding a pack-and-play crib or renovating a room.
8. I make the selected change in Airbnb or invest in the physical property.
9. I wait and monitor whether occupancy or revenue improves, but I do not currently have a reliable way to attribute any performance change to the specific action I took.

### 5. Where it breaks

**Question:** Where does the workflow slow down, fail, create rework, or frustrate the user?

The workflow breaks down in three places. First, I do not have a consistent decision framework for deciding which listing or property changes to prioritize. I compare listings manually and then rely on judgment and expert videos to interpret gaps, so the process can be subjective and difficult to repeat consistently.

Second, comparing 5–15 Airbnb listings is time-consuming. I need to open and review multiple listing pages, visually compare photos, content, amenities, prices, and settings, and manually record the relevant differences. For this capstone, I will manually capture the comp data because Airbnb does not provide an API or MCP for this use case and does not permit screen scraping.

Third, I cannot reliably measure the impact of a specific change. There can be a long lag between changing a photo, description, amenity, or property feature and seeing any change in occupancy or revenue. My revenue increased between 2025 and 2026, but I cannot make a concrete connection between that increase and individual listing changes or capital improvements. The MVP will not solve live outcome attribution; instead, it will make the recommendation and prioritization step more evidence-backed, consistent, and reviewable.

### 6. Why an agent

**Question:** What should the agent help with, and why is an agent a better fit than a static AI feature?

The agent should help me identify which part of my Airbnb listing deserves attention first—photos, description, amenities, or pricing positioning—and then assemble the evidence needed to support that decision. It should compare my listing with the relevant evidence from 10–15 nearby competing listings, including listing text, amenities, price positioning, and AI-generated photo descriptions, and use trusted short-term-rental YouTube transcripts where expert guidance is relevant. Rather than present every available data point, it should retrieve the evidence most relevant to the claim it is making and produce a specific, prioritized recommendation, such as changing a photo, rewriting a description line, or adding or removing an amenity.

Before showing me a recommendation, the agent should check that its cited comp or expert evidence actually supports the claim. If the available evidence is weak, missing, or contradictory, it should flag that uncertainty rather than guess. This gives me a recommendation I can personally review without needing deep short-term-rental expertise.

An agent is a better fit than a static AI feature because this workflow requires a sequence of decisions and checks, not a single prompt-and-response. The system must first decide what evidence to retrieve from three distinct sources—comp listing text and amenities, comp photo descriptions, and YouTube transcripts—based on the listing area being evaluated. It then needs to generate a recommendation, verify each citation against its source, and revise, remove, or flag unsupported claims. The workflow also coordinates multiple steps, including vision-based photo description, retrieval, recommendation generation, and self-checking. A lightweight plan → retrieve → generate → self-check loop is therefore more appropriate than a one-shot prompting feature; it provides the orchestration and evidence validation needed to make recommendations consistent, grounded, and reviewable.

### 7. Safe fake data

**Question:** What synthetic data, policies, examples, or cases will you create so the project is safe to build and demo?

I will use a fixed, manually captured dataset of my own Airbnb listing and 10–15 nearby competing listings for the capstone demo. I will snapshot my own listing at the start of the project so the agent and evaluation set compare against a stable baseline, even if I later act on recommendations. Because competing listings belong to other hosts, I will anonymize them in the prototype, demo, and write-up as “Comp 1,” “Comp 2,” and so on; I will not show listing names, exact addresses, host identities, or guest names. Any guest review text included in the corpus will have names removed.

I will create synthetic adversarial cases alongside the real comp data to test whether the agent behaves safely. One case will make an apparently plausible recommendation unsupported by the available evidence; the expected behavior is for the agent to state that evidence is insufficient rather than invent a citation. Another case will include a subtly mismatched citation—for example, evidence from the correct comp that does not support the specific claim—to test whether the self-check step catches and removes or flags it.

The agent will follow a no-citation-no-claim policy: it cannot present a recommendation unless it cites specific supporting comp evidence or an approved expert source. If it cannot find adequate grounding, or if evidence is conflicting, it must say so explicitly rather than fill the gap with general knowledge. For YouTube expert material, I will store paraphrased or summarized claims rather than reproduce transcript text verbatim. The agent will identify the supporting video and timestamp without relying on long direct quotes. These policies let me demonstrate grounded recommendations without exposing third-party identities, using copyrighted material unnecessarily, or presenting unsupported advice as fact.

### 8. Where humans stay in control

**Question:** What is the agent not allowed to do? When must a human approve, edit, reject, or escalate?

The agent is not allowed to make changes to my Airbnb listing, PriceLabs pricing, PriceLabs pricing rules, or my property without my explicit approval. It may analyze my fixed comp dataset, retrieve relevant expert evidence, and recommend a prioritized action, but it cannot publish or edit listing content. For example, if it recommends changing photo order, rewriting a description line, or adding or removing an amenity, I review, edit, approve, reject, and manually make the change in Airbnb.

The agent may use PriceLabs information as evidence for pricing positioning, and PriceLabs can support MCP-based pricing actions, but the agent must not change a price or pricing rule unless I specifically approve that action first. Similarly, recommendations involving capital spending or physical property upgrades—such as buying furniture, adding an amenity, or renovating a room—require my approval before any action moves forward.

The agent must also escalate to me rather than guess when evidence is insufficient, conflicting, or unsupported by a valid citation. Its role is to provide grounded, reviewable recommendations; my role is to make the final decision and execute or authorize every external change.

### 9. How you know it works

**Question:** What is one practical metric that would show the agent is useful?

I will measure the percentage of agent recommendations that pass my manual groundedness check on the first evaluation run. A recommendation passes only when I can verify that its cited comp evidence or approved YouTube source directly supports the specific claim and proposed action; unsupported, mismatched, or missing citations fail.

I will calculate: (number of recommendations that pass the groundedness check ÷ total recommendations produced) × 100. This is practical because I can score it in an afternoon using my 10–15-scenario evaluation set, including adversarial cases, without needing booking or occupancy outcomes that will not be available within five weeks. A high pass rate shows the agent is retrieving and checking evidence rather than guessing; a low pass rate shows that its recommendations are not yet trustworthy enough for me to use.

### 10. What people will see

**Question:** What will the demo visibly show from input to agent work to human review?

The demo will visibly show one complete, reviewable agent workflow from fixed input to human decision support.

First, I will show the snapshot of my own Airbnb listing used as the stable baseline for the capstone: its title, description, amenities, and photos. I will then show the fixed, anonymized dataset of 10–15 nearby competitors, labeled “Comp 1,” “Comp 2,” and so on, rather than exposing other hosts’ listing names, addresses, or identities.

Next, I will run the agent live against that fixed dataset rather than only reveal a prewritten final answer. The screen will show the agent selecting a listing dimension to evaluate—for example, photos—retrieving the relevant comp records and AI-generated photo descriptions, and drafting a specific recommendation. It will then run its self-check against the cited comp evidence or approved YouTube source before presenting the recommendation. I will make this evidence-checking step visible so viewers can see that the agent is following a plan → retrieve → generate → self-check loop, rather than producing a one-shot response.

For human review, I will place the recommendation beside the specific cited comp evidence or YouTube source and manually verify that the source supports the claim and proposed action. I will also demonstrate an adversarial case in which evidence appears plausible but does not actually support the claim; the expected result is that the agent flags insufficient evidence or removes the unsupported recommendation rather than guessing.

I will close by reporting the groundedness result from my first evaluation run: the percentage of recommendations whose cited evidence directly supports the specific claim and proposed action. This shows not only what the prototype recommends, but whether I can trust and verify its recommendations before deciding whether to make any Airbnb, PriceLabs, or property change.

## Design

### 11. Job to be done

**Question:** What job is the agent being hired to do?

The single end-to-end loop my prototype will prove is the photo-analysis loop. I chose it because I can fully validate the evidence myself: I can visually compare my listing with anonymized comps and assess photo order, furnishing condition, and visual cohesion. My concrete example is dated living-room furniture and weaker photo ordering in my listing compared with stronger comps that lead with cohesive, updated furnishings.

For the capstone, one complete loop means the agent takes my frozen listing snapshot, retrieves relevant anonymized comp records and AI-generated photo descriptions, identifies a photo-related gap, and drafts a specific recommendation. The recommendation may propose reordering photos, replacing a photo, or flagging a furnishing gap as a potential capital improvement. It cites the actual comp evidence it used and runs a self-check to confirm whether that evidence directly supports the claim before presenting the result.

The minimum prototype surface is a map showing 2–3 recommendation cards from this one photo loop. Each card shows one recommendation type and makes the self-check visible rather than burying it in a report. It includes the proposed action; a clear, paired comparison between my listing and the relevant comp or comps; the cited evidence, including the comp label and AI-generated photo-description text or the image where shown; and a plain statement of confidence and evidence gaps. Each card also has a distinct self-check result, such as “Citation verified: comp evidence supports this claim” or “Insufficient evidence — flagged for review.” I can approve, reject, or request revision for each card.

This proves the complete loop from fixed input, through evidence retrieval and a grounded recommendation, to a human decision. The agent does not make listing changes or research purchase options. If it identifies a furnishing gap, it can flag it as a potential capital improvement that needs human review, but it does not research couches or other purchases.

I am deliberately keeping the following work out of scope for this five-week build. Amenities, settings, listing-copy, guest-review, and pricing loops follow the same pattern but are documented for later rather than implemented. The feasibility and investment engine—live search for products or services, budget matching, cost, delivery, and timing research—is also deferred. I will not build the broader action tracker, parking lot, holistic comp-review panel, live PriceLabs-refresh panel, or expert-insights panel. Persistent cross-session memory is also deferred; a simple log of what happens during the one demo run is sufficient.

These are deferred ideas, not rejected ones. I am preserving that distinction so the capstone remains focused on proving one complete, reviewable photo-analysis loop rather than quietly expanding into a broader product build.

### 12. Future process steps

**Question:** How does the workflow change when the agent is introduced? List the future process as text steps.

The agent will evaluate my fixed market-comp dataset and PriceLabs competitive pricing and occupancy information to identify evidence-backed factors that may be affecting my listing’s performance. It will assess relevant dimensions of my listing—including photos, description, amenities, Airbnb settings and features, pricing positioning, and possible capital improvements—against 10–15 nearby anonymized comparable listings. For each dimension, it will characterize my listing as below the market benchmark, meeting the benchmark, or potentially best in class, based only on cited comp evidence and approved short-term-rental expert guidance that I identify from YouTube.

The agent will produce a prioritized list of recommended changes. Each recommendation will state what I should consider changing, why it is recommended, the specific comp or expert evidence that supports it, and any uncertainty or evidence gaps. It will retrieve only the evidence relevant to the claim, self-check that every citation directly supports the recommendation, and flag insufficient or conflicting evidence rather than guess.

I will review the recommendations, ask questions, and provide feedback. The agent may refine the recommendation list and priority based on that feedback, but it cannot make changes on its own. I choose which recommendations to implement and manually approve or execute any Airbnb content change, PriceLabs pricing or pricing-rule change, amenity purchase, or capital improvement.

Over the longer term, after I tell the agent which approved changes I implemented and when, it can help me maintain a change log and monitor signals such as revenue, occupancy, ADR, reviews, and page views. These measures are future monitoring signals rather than proof of causal impact in this five-week MVP; the capstone’s primary success metric remains the percentage of recommendations that pass my manual groundedness check.

### 13. Observe, decide, act, check

**Question:** What does the agent observe, reason about, produce, and check before handing work back?

The agent operates as an evidence-backed, human-reviewed loop: observe, reason, produce, check, and hand work back to me for a decision.

**Observe:** The agent receives my fixed baseline listing snapshot—title, description, amenities, photos, relevant Airbnb settings, and anonymized guest reviews—plus a fixed, anonymized dataset of 10–15 nearby comparable listings. Each comp record can include listing text, amenities, settings, prices and relevant PriceLabs competitive pricing and occupancy information, AI-generated photo descriptions, and anonymized guest reviews. I also provide approved short-term-rental expert guidance from YouTube. Guest names and identifying details are removed, and the capstone demo uses fixed, manually captured data rather than a live data-collection pipeline.

**Reason and decide:** The agent evaluates my listing in this order: photos, amenities, Airbnb settings and features, listing copy, guest-review themes, and pricing positioning. For each dimension, it compares my listing with relevant stronger comps and assesses whether I appear below the market benchmark, meet the benchmark, or may be best in class. It identifies potential gaps, distinguishes between low-effort listing changes and potential capital improvements, and prioritizes recommendations by the strength and relevance of the evidence. It does not claim that a correlation in comp data proves a change will increase occupancy or revenue.

For example, in the photo loop, the agent compares my photo order and AI-generated photo descriptions with those of stronger comps. It may observe that several stronger comps lead with well-presented living spaces featuring newer, cohesive furniture, while my furniture appears dated or my strongest living-space photos appear later in the sequence. It then decides whether the evidence points to a low-effort presentation change, such as reordering existing photos, or a potential capital improvement, such as evaluating a furniture upgrade. A competitor’s newer furniture is evidence of a possible market gap, not proof that purchasing furniture will increase revenue.

In the amenities loop, the agent compares the amenities shown in my listing with those common among stronger relevant comps and can recommend that I investigate an amenity gap when the comparison is cited. In the settings loop, it compares relevant Airbnb settings or features and may recommend that I review a setting, while leaving all changes for my approval. In the listing-copy loop, it compares titles and descriptions with competitor positioning and approved expert guidance, then recommends a specific content change only when the evidence supports it. In the guest-review loop, it identifies recurring anonymized themes in my reviews and those of relevant stronger comps—for example, positive comments about comfort or repeated concerns about a space—and uses those themes to support a recommendation or identify an issue to investigate. Review themes are supporting evidence, not objective proof of a performance driver. Pricing is evaluated last because I already use PriceLabs to optimize daily pricing; the agent uses PriceLabs information to assess pricing positioning and identify questions for my review, not to replace PriceLabs or change prices or pricing rules.

For possible capital improvements or amenity purchases, the agent runs a feasibility and investment loop. It uses my stated budget, delivery constraints, and implementation preference, such as DIY versus using a professional, along with approved online research sources to compare current purchase cost, delivery, installation requirements, and estimated time to complete the change. For example, if I have a $500 budget for a new couch and can receive delivery myself, the agent can identify options within that constraint and show the trade-offs. It can rank the opportunity as prioritize, investigate, or defer based on evidence strength, feasibility, and my constraints, but it cannot invent or guarantee an ROI.

**Produce:** The agent returns a prioritized recommendation list. Each recommendation states the listing dimension, the proposed change or investigation, why it is prioritized, whether my listing is below benchmark, meeting benchmark, or potentially best in class, the cited comp, review, and/or approved expert evidence, and any uncertainty or evidence gap. For a purchase or capital improvement, it also states the applicable budget, source options, delivery or installation assumptions, estimated effort or timing, and whether it fits my constraints. It can answer my follow-up questions and refine the ranking based on my feedback.

**Check before handoff:** Before showing a recommendation, the agent self-checks whether each cited source directly supports the specific claim and proposed action. It also checks that any product, delivery, installation, cost, and timing details are current, cited, and consistent with the budget and implementation constraints I provided. If evidence is missing, conflicting, weak, or does not support the recommendation, the agent must flag insufficient evidence, lower its confidence, or omit the recommendation rather than guess. I then review the cited evidence myself, approve, reject, or edit recommendations, and manually make any Airbnb, PriceLabs, amenity, or capital-improvement change. The agent cannot make changes on my behalf.

### 14. What the agent needs

**Question:** What information, examples, rules, files, or user inputs does the agent need to perform well?

The agent needs five categories of information to perform well: a stable market-comparison dataset, trusted guidance, clear decision rules, my feasibility constraints, and sources it can cite.

First, it needs a fixed snapshot of my own Airbnb listing: title, description, amenities, photos, relevant Airbnb settings and features, and anonymized guest reviews. It also needs a fixed, anonymized dataset of 10–15 nearby comparable listings. Each comp record can include listing text, amenities, settings, prices, relevant PriceLabs competitive pricing and occupancy information, AI-generated photo descriptions, and anonymized guest reviews. Competitors are labeled only as Comp 1, Comp 2, and so on; listing names, exact addresses, host identities, guest names, and other identifying information are removed.

Second, it needs approved short-term-rental expert guidance, such as selected YouTube transcripts, as supplementary evidence. It must use this guidance only when it is relevant to a specific recommendation and cite it alongside the comp evidence it relies on. The agent should retrieve only the information relevant to the dimension under review rather than treat all available data as equally important.

Third, it needs explicit comparison and safety rules. It evaluates my listing in this order: photos, amenities, Airbnb settings and features, listing copy, guest-review themes, and pricing positioning. For each dimension, it compares my listing with relevant stronger comps and labels my position as below the market benchmark, meeting the benchmark, or potentially best in class. It must distinguish evidence from inference: competitor patterns and review themes can identify a possible gap, but they do not prove that a change will increase occupancy or revenue. It must cite the evidence supporting every claim and recommendation, flag conflicting or insufficient evidence, and never make or publish changes to Airbnb or PriceLabs.

For example, the agent may find that stronger comps prominently show newer, cohesive living-room furniture while my furniture appears dated. It can recommend that I first improve photo order if my strongest living-space image is not leading, or flag a furniture upgrade as a potential capital improvement. It cannot claim that a new couch will generate a particular revenue gain without evidence that supports that claim.

Fourth, the agent needs my decision constraints for potential purchases and capital improvements. I provide the available budget, whether I plan to do work myself or hire a professional, delivery and installation constraints, and other requirements relevant to the decision. Budget is the primary constraint. For example, if I have a $500 budget for a couch and can receive delivery myself, the agent should use those constraints when researching options. If the option most consistent with the competitive evidence costs more than my budget, the agent must call that out clearly. It should distinguish between: an option that fits my budget and addresses the gap; a lower-cost alternative that only partially addresses it; and the market-appropriate option that is currently out of budget. It can recommend that I prioritize, investigate, defer, or reconsider the budget, but it cannot disguise a lower-cost substitute as equivalent.

Fifth, the agent needs access to approved, citable sources for feasibility research. For a potential furniture purchase or amenity addition, it can use online product and service sources such as Amazon, Wayfair, or Angi to gather current price, availability, delivery, installation requirements, and estimated timing. It must record the source and date of the information, check that it fits the constraints I provided, and identify uncertainty when information is unavailable or changes.

The agent’s output should be a prioritized, reviewable recommendation list. Each recommendation needs the listing dimension, proposed change or investigation, the relevant market benchmark, cited comp, review, and/or expert evidence, confidence or uncertainty, and the reason it ranks where it does. For an amenity purchase or capital improvement, the output also needs the applicable budget, source options, cost, delivery or installation assumptions, estimated time or effort, and a clear indication of whether the best-supported option fits the budget. I review the evidence and make every final decision and change myself.

### 15. Actions the agent can take

**Question:** What tools, files, systems, or mock actions will the prototype use? Text descriptions are enough.

The prototype will use provided files, MCP-connected evidence sources, controlled web search, and human-approved mock actions.

I will provide fixed files containing a snapshot of my own Airbnb listing and an anonymized dataset of 10–15 nearby comparable listings. These files will include relevant listing text, amenities, photos or AI-generated photo descriptions, Airbnb settings, and anonymized guest-review data. The files are the fixed evidence base for the capstone demo; competitor names, exact addresses, host identities, guest names, and other identifying information are removed.

The agent will access PriceLabs competitive pricing and occupancy information through MCP. It will use this information to assess pricing positioning and competitive context, but it will not replace PriceLabs, change daily prices, or modify PriceLabs rules. The agent will also access approved short-term-rental YouTube transcript data through MCP. It can retrieve and cite relevant expert guidance when it supports a specific recommendation, but it cannot treat general expert advice as proof that a change will improve listing performance.

The agent will have controlled web-search access for feasibility research on amenities and capital improvements. It can search sources such as Amazon, Wayfair, or Angi to identify current product or service options and collect citable information about price, availability, delivery, installation requirements, and expected timing. I provide the decision constraints, especially budget and whether I plan to use a DIY or professional approach. For example, if a couch that best matches the competitive evidence costs more than my $500 budget, the agent must state clearly that the market-appropriate option is out of budget. It must distinguish that option from a lower-cost alternative that only partially addresses the gap, rather than presenting the cheaper option as equivalent.

The agent can take these mock actions: create a cited, prioritized recommendation; draft a proposed listing-content or photo-order change; create a project proposal for an amenity or capital improvement; search for options that fit my stated constraints; ask me for missing constraints; and update a recommendation based on my feedback. It cannot publish or edit Airbnb content, change PriceLabs prices or rules, purchase a product, book a service, schedule work, or make any other external change.

Every proposed listing change or property project goes through an approval workflow. I can approve, reject, or request revision, and the prototype records the recommendation, evidence, confidence or uncertainty, my decision, and the intended next step in a reviewable action log. Examples include “approved: reorder living-room photos,” “rejected: change minimum-stay setting,” and “approved: investigate couch options within a $500 budget.” After I manually make an approved Airbnb change or complete a property project outside the prototype, I can mark the action as completed in the log. This preserves a visible record of what the agent recommended, what I decided, and what was actually done.

### 16. What should persist

**Question:** What should the agent remember, and what should it not remember?

The agent should retain decision-relevant memory that helps it improve recommendations over time, while keeping the fixed capstone evidence base separate from changing preferences and decisions.

It should remember my feedback on each recommendation, including whether I approved, rejected, requested revision, or later marked the action as completed. For rejected recommendations, it should record the reason: insufficient evidence, too expensive, too much effort, not relevant to my property, or my free-text explanation. It should use this feedback in later runs—for example, by avoiding a recommendation I have already rejected for being out of budget unless there is materially new evidence, a different lower-cost option, or I change the budget.

The agent should remember my stable decision preferences and constraints, including my budget, whether I prefer a DIY or professional approach, delivery and installation constraints, and the evaluation order I use: photos, amenities, Airbnb settings and features, listing copy, guest-review themes, and pricing positioning. It should also retain the action log: the recommendation, evidence cited, confidence and uncertainty, my decision, intended next step, and whether I manually completed the approved action. Completed-action history should remain available ongoing so I have a durable record of what the agent suggested, what I decided, and what I actually changed; it also prevents the agent from recommending already completed work as though it were still outstanding.

The agent should remember when a recommendation depends on a specific constraint or piece of evidence, and it should date that memory. Budget, product availability, delivery timing, PriceLabs data, competitor information, and market conditions can change, so the agent must treat them as time-sensitive and ask for confirmation or refresh the evidence when needed.

The agent should not retain unnecessary personal or sensitive data. It should not store guest names, host identities, exact competitor addresses, payment information, account credentials, or raw identifying review content. It should not treat a rejected recommendation as a permanent rule without preserving the reason and allowing me to edit or remove that preference. It also should not remember unsupported inferences as facts, such as claiming that a furniture change increased revenue unless I later provide evidence that supports that conclusion.

I can review, edit, or delete the agent’s remembered preferences, constraints, feedback, and action history. The agent cannot make changes to Airbnb, PriceLabs, purchases, or property projects based on memory alone; every new recommendation remains subject to evidence checks and my explicit approval.

### 17. Reviewable result

**Question:** What should the agent produce so a human can review it quickly and confidently?

The agent should produce a visible, reviewable recommendation workspace that helps me make decisions quickly and keeps the evidence, decisions, and outcomes in one place.

For each recommendation, the agent should show the type of change, such as photo order, listing copy, amenity, Airbnb setting, pricing-positioning question, or capital improvement; the recommended action and its priority; why it is recommended; proof points from relevant anonymized comparable listings and approved expert YouTube guidance; and a direct comparison with my property, including whether I am below the market benchmark, meeting it, or potentially best in class. It should include images or visual comparisons where helpful, links or citations to the underlying evidence, confidence and evidence gaps, and the date each source was checked.

Each recommendation should also show potential impact if implemented. The agent may provide an ROI estimate only when the available evidence and stated assumptions support one. It must clearly distinguish an assumption-based estimate from a measured result or guaranteed outcome, and it must not invent ROI. Where a recommendation is not appropriate now, the agent should state why—for example, insufficient evidence, budget constraints, excessive effort, or a stronger competing priority.

The workspace should let me give a thumbs up or thumbs down, approve, reject, request revision, or place a recommendation in a parking lot for later. For a rejection or deferral, I should be able to record why, including insufficient evidence, too expensive, too much effort, not relevant to my property, or a free-text explanation. The agent should retain and use this feedback in future recommendations.

Approved recommendations should move into an action tracker. Each approved action should retain its cited evidence, decision date, owner, next step, target completion date if applicable, and success measures. Occupancy is my primary success measure. Before I manually implement a change, the workspace should capture a dated PriceLabs baseline for occupancy, with conversion and revenue retained as supporting metrics. After implementation, the agent can refresh current occupancy, conversion, and revenue data through PriceLabs MCP and compare it with the baseline over a stated time window. It must not claim that a single change caused an occupancy, conversion, or revenue result without sufficient evidence and context.

After I make the change manually, I can mark it completed and record the result against the baseline. Completed-action history remains available ongoing so the agent can avoid re-recommending work that has already been done and so I can review what changed over time.

The workspace should also include a holistic comp-data area where I can review my listing against the 10–15 anonymized comparable listings by dimension, including photos, amenities, settings, copy, guest-review themes, and pricing positioning. I should be able to refresh, update, add, or remove comp records from the evidence set while preserving the date and provenance of each record.

A separate PriceLabs area should allow me to refresh current competitive pricing, occupancy, conversion, and revenue information through MCP. The agent may use refreshed PriceLabs evidence to update its pricing-positioning analysis, but it cannot change prices or PriceLabs rules. A separate expert-insights area should highlight newly available or newly relevant ideas from approved YouTube transcript sources, clearly separating expert guidance from comp evidence and showing why the idea may be relevant to my property.

The agent’s output remains decision support, not autonomous execution. Every Airbnb listing change, PriceLabs action, purchase, or property project requires my explicit approval and manual completion.

### 18. When the agent should stop

**Question:** What should happen when the agent is unsure, missing data, or facing a risky case?

The agent should stop, flag the case for human review, and avoid making a definitive recommendation when critical evidence is missing, conflicting, stale, or insufficient to support the claimed action. Human review is a required guardrail because the agent is decision support for my Airbnb listing and property investments, not an autonomous decision-maker or executor.

Critical evidence depends on the recommendation type. For a listing-content, photo-order, amenity, or settings recommendation, the agent needs relevant comparison evidence from my listing and the anonymized comp dataset, plus citations that directly support its claim. For a pricing-positioning recommendation, it needs current relevant PriceLabs data. For a potential purchase or capital improvement, it needs evidence of the competitive gap, my stated budget and feasibility constraints, and current citable option details such as cost, availability, delivery, installation requirements, and timing. If any critical input is unavailable, contradictory, outdated, or too weak to support the recommendation, the agent must not fill the gap with assumptions.

For example, the agent may observe that stronger comparable listings appear to have newer living-room furniture, but it cannot claim that buying a new couch will improve occupancy or produce a specific ROI unless it has evidence and assumptions that support that estimate. If it cannot determine whether an appropriate couch fits my budget, or if the relevant options are unavailable, it should label the recommendation “needs human review,” show the evidence it does have, identify exactly what is missing, and offer limited next steps: provide the missing constraint or evidence, refresh the relevant data, conduct additional research, defer the idea to the parking lot, or revise the budget. It should clearly state when the market-appropriate option is out of budget and distinguish it from a lower-cost alternative that only partially addresses the gap.

The same rule applies when sources conflict. The agent should present the conflicting comp evidence, PriceLabs data, or expert guidance, explain why it cannot resolve the conflict, and ask me to decide how to proceed. It should not use a confident priority ranking, ROI estimate, or causal claim when critical evidence is missing or unresolved.

After the agent completes its analysis, I review its proposed recommendations in the UI. For each recommendation, I can approve it, reject it, request a revision, defer it to the parking lot, or, after I manually carry it out, mark it complete. The UI records the recommendation, supporting evidence, uncertainty, my decision, and the next step. The agent uses my feedback and completed-action history in later runs, but it cannot publish or edit Airbnb content, change PriceLabs prices or rules, make purchases, schedule services, or begin a property project. Every external change requires my explicit approval and manual completion.

### 19. Decision checkpoint

**Question:** Where does the human approve, edit, reject, or escalate the agent's work?

The human decision checkpoint happens after the agent completes its analysis and presents proposed recommendations in the UI. I review each recommendation before any change is made to my Airbnb listing, PriceLabs settings, purchases, or property projects.

For each recommendation, the UI shows the proposed action, recommendation type, rationale, supporting comp-listing and expert evidence, comparison with my property, uncertainty or missing evidence, and the proposed next step. I can approve it, reject it, request a revision, defer it to a parking lot for later, or, after I manually carry it out, mark it complete. The UI records my decision, feedback, and intended next step in the action history.

Human review is also a required guardrail when critical evidence is missing, conflicting, stale, or insufficient. In those cases, the agent must label the item “needs human review,” identify what evidence is missing or unresolved, show the evidence it does have, and avoid a definitive recommendation, confident priority ranking, ROI estimate, or causal claim. I can then provide a missing constraint or evidence, refresh the data, request additional research, defer the item, or revise a constraint such as budget.

For example, if the agent finds that stronger comparable listings appear to have newer living-room furniture but cannot establish that a new couch fits my budget or would improve occupancy, it should not claim a specific ROI. It should show the competitive evidence, identify the budget or outcome-evidence gap, and ask me whether to research more, revise the budget, or defer the idea.

The agent uses my approvals, rejections, revision requests, deferrals, and completed-action history to improve later recommendations. It cannot publish or edit Airbnb content, change PriceLabs prices or rules, make purchases, schedule services, or begin a property project. Every external change requires my explicit approval and manual completion.

### 20. How you will test judgment

**Question:** What cases will prove the agent works, respects boundaries, and handles edge cases?

I will test the agent’s judgment with a fixed set of 10–15 scenarios drawn from my anonymized comp dataset, PriceLabs information, approved expert YouTube transcripts, and adversarial cases. Each scenario will have an expected outcome: make a grounded recommendation, ask for human review, or decline to make a recommendation. I will manually score whether the agent selected relevant evidence, cited it accurately, respected its boundaries, and avoided unsupported claims.

A passing recommendation must identify a specific listing, settings, amenity, photo, pricing-positioning, or property-improvement opportunity; compare my property with relevant anonymized comps; cite supporting comp and expert evidence where applicable; explain the reasoning; state uncertainty; and avoid claiming that an action will cause an occupancy, conversion, revenue, or ROI result unless the evidence and assumptions support that estimate. I will calculate groundedness as: (recommendations that pass my manual groundedness check ÷ total recommendations produced) × 100.

I will include straightforward cases where the evidence supports a recommendation. For example, if 8 of 10 stronger comparable listings show a dedicated workspace and approved expert guidance identifies a work-friendly setup as relevant, the agent may propose adding and photographing a small workspace. The recommendation must show the comp and expert proof points, how my listing differs, relevant images or visual evidence where available, and a proposed next step.

I will also test uncertainty and human-in-the-loop behavior. In the workspace example, if the agent does not know whether there is enough room, what furniture is feasible, or what I am willing to spend, it must not claim that the change will increase occupancy or produce a specific ROI. It should label the item as needing human review, identify the missing constraints, and present a project-specific proposed budget range based on the competitive gap, available options, and stated assumptions. I can then approve, revise, reject, or defer that budget and recommendation in the UI. The agent should update its recommendation only after receiving my feedback or refreshed evidence.

My edge-case set will include missing evidence, conflicting sources, stale PriceLabs information, a comp pattern supported by too few relevant listings, expert advice that does not fit my property, out-of-budget options, unavailable products, and recommendations that have already been rejected or completed. In these cases, the expected behavior is to show the available evidence and uncertainty, explain what is missing or conflicting, request a human decision or a data refresh, or defer the idea to the parking lot. It must not invent facts, fill gaps with assumptions, present a confident ranking when critical evidence is unresolved, or repeat completed work as a new recommendation.

I will explicitly test the agent’s boundaries. It may analyze evidence, retrieve approved guidance, draft a recommendation, propose a project budget, and record my feedback. It may not publish or edit Airbnb content, change PriceLabs prices or rules, make purchases, schedule services, or begin a property project. After analysis, I review each proposed recommendation in the UI and can approve, reject, request revision, defer it to a parking lot, or mark it complete after I manually carry it out.

For approved actions, I will record a dated PriceLabs baseline before implementation. Occupancy is my primary success measure, with conversion and revenue as supporting measures. I can refresh those metrics through PriceLabs MCP after implementation and compare them over a stated time window, while treating the results as observational rather than automatically attributing changes to one recommendation. The agent passes this judgment test when its recommendations are grounded, its uncertainty handoffs are appropriate, and it consistently respects the human approval and no-execution boundaries.

## Develop

### 21. One end-to-end loop

**Question:** What single end-to-end loop will the prototype prove?

The single end-to-end loop my prototype will prove is the photo-analysis loop. I chose it because I can fully validate the evidence myself: I can visually compare my listing with anonymized comps and assess photo order, furnishing condition, and visual cohesion. My concrete example is dated living-room furniture and weaker photo ordering in my listing compared with stronger comps that lead with cohesive, updated furnishings.

For the capstone, one complete loop means the agent takes my frozen listing snapshot, retrieves relevant anonymized comp records and AI-generated photo descriptions, identifies a photo-related gap, and drafts a specific recommendation. The recommendation may propose reordering photos, replacing a photo, or flagging a furnishing gap as a potential capital improvement. It cites the actual comp evidence it used and runs a self-check to confirm whether that evidence directly supports the claim before presenting the result.

The minimum prototype surface is a map showing 2–3 recommendation cards from this one photo loop. Each card shows one recommendation type and makes the self-check visible rather than burying it in a report. It includes the proposed action; a clear, paired comparison between my listing and the relevant comp or comps; the cited evidence, including the comp label and AI-generated photo-description text or the image where shown; and a plain statement of confidence and evidence gaps. Each card also has a distinct self-check result, such as “Citation verified: comp evidence supports this claim” or “Insufficient evidence — flagged for review.” I can approve, reject, or request revision for each card.

This proves the complete loop from fixed input, through evidence retrieval and a grounded recommendation, to a human decision. The agent does not make listing changes or research purchase options. If it identifies a furnishing gap, it can flag it as a potential capital improvement that needs human review, but it does not research couches or other purchases.

I am deliberately keeping the following work out of scope for this five-week build. Amenities, settings, listing-copy, guest-review, and pricing loops follow the same pattern but are documented for later rather than implemented. The feasibility and investment engine—live search for products or services, budget matching, cost, delivery, and timing research—is also deferred. I will not build the broader action tracker, parking lot, holistic comp-review panel, live PriceLabs-refresh panel, or expert-insights panel. Persistent cross-session memory is also deferred; a simple log of what happens during the one demo run is sufficient.

These are deferred ideas, not rejected ones. I am preserving that distinction so the capstone remains focused on proving one complete, reviewable photo-analysis loop rather than quietly expanding into a broader product build.

### 22. What the user does

**Question:** What will the user type, upload, click, or review in the prototype?

I am the initial user and human reviewer of the prototype. At the beginning of a run, I upload one spreadsheet containing a frozen snapshot of my own Airbnb listing and the manually collected, anonymized data for comparable units. My listing data includes its relevant details and photos or photo references; comp records include the information needed for the photo-analysis loop, including AI-generated photo descriptions or images where available. I also provide the approved short-term-rental expert YouTube pages or transcripts the agent may use as guidance.

The agent can access PriceLabs through MCP for relevant rates, occupancy, and competitive context, which can be refreshed in real time where relevant. The uploaded spreadsheet remains the fixed evidence base for the capstone photo-analysis loop; PriceLabs data is supporting context rather than a replacement for the frozen visual comparison dataset.

After uploading the spreadsheet, I click “Run photo analysis.” The agent retrieves the relevant listing and comp records, evaluates photo order, furnishing condition, and visual cohesion, and returns 2–3 recommendation cards. Each card shows the proposed action, a paired comparison between my listing and the relevant comp or comps, the cited comp photo-description evidence or images where available, confidence and evidence gaps, and a visible self-check result such as “Citation verified: comp evidence supports this claim” or “Insufficient evidence — flagged for review.”

I review each card and inspect the source evidence before choosing one of three actions: approve, reject, or request revision. The prototype records what happens during that demo run, but it does not publish listing changes, alter PriceLabs settings, make purchases, or carry out any external action.

### 23. Demo-safe inputs

**Question:** List the fake data files, sample records, policies, or examples used in the prototype.

I will use one demo-safe spreadsheet as the starting input for each prototype run. It contains one record for my Airbnb unit and five manually collected comparable-unit records. The spreadsheet includes these columns: `listing_label`, `is_my_listing`, `airbnb_id`, `airbnb_url`, `avg_price_pricelabs`, `min_price_pricelabs`, `max_price_pricelabs`, `occ_pct_approx_pricelabs`, `n_nights_tracked`, `description`, `amenities`, `bedroom_count`, `bathroom_count`, `review_count`, `review_rating`, `review_text_sample`, `photo_count`, `photo_urls`, `photo_ai_descriptions`, `selected_for_deep_data`, and `notes`.

The file gives the prototype the fixed evidence it needs for the photo-analysis loop. It identifies my listing with `is_my_listing` and provides the comparable listings’ descriptive, amenity, review, pricing, occupancy, and photo-related evidence. The photo-analysis loop relies especially on `photo_urls` and `photo_ai_descriptions` to compare photo order, furnishing condition, and visual cohesion between my listing and relevant comps. PriceLabs fields provide supporting market context, including approximate occupancy, average price, price range, and nights tracked.

Before use in the prototype and demo, I will anonymize competitor records: I will not display competitor listing names, exact addresses, host identities, guest names, or identifying review details. Competitors will be shown as labels such as “Comp 1” through “Comp 5.” I will also remove or redact any sensitive information from review samples and notes. The spreadsheet is a manually collected, frozen snapshot for the capstone rather than a live Airbnb data feed.

After I upload the spreadsheet, I click “Run photo analysis.” The agent selects relevant records, generates 2–3 photo-related recommendation cards, and shows the paired listing-versus-comp evidence, cited photo descriptions or images where available, confidence and evidence gaps, and a visible citation self-check. I then approve, reject, or request revision; the prototype records that decision for the demo run only.

### 24. Test set

**Question:** List at least five test cases, including happy path, edge case, and boundary case.

I have not tested the agent yet. I will test the photo-analysis loop against a fixed set of at least five scenarios using my uploaded spreadsheet, which contains my listing and five real comparable units, their photo URLs, AI-generated photo descriptions, and available PriceLabs occupancy and revenue fields.

Before each test, I will define the expected result and require the agent to use a consistent response format. Every response must include:

1. A specific recommendation. For example, it might recommend moving a named living-room photo into the first position rather than giving general advice to improve photos.
2. Evidence. The agent must cite at least one higher-performing comparable listing and its relevant occupancy or revenue data, then explain the relevant photo comparison. It may also cite approved short-term-rental expert YouTube guidance when that guidance directly supports the proposed action. Higher performance is supporting comparison evidence, not proof that the photo alone caused the result.
3. A confidence level of high, medium, or low, with a brief explanation based on the strength, consistency, and completeness of the available evidence.

For example, in a clear photo-order-gap scenario, the agent should identify that my listing leads with an exterior close-up while one or more higher-performing comps lead with clear, cohesive full-room living-area images. It should recommend a specific change, such as moving my clearest full-room living-room photo to the first position; cite the comparable listings’ occupancy or revenue data and photo evidence; and state an appropriately qualified confidence level. It must not guarantee that the change will increase revenue or occupancy.

A test passes only if the agent completes every item in that scenario’s expected result. If it misses one or more items—such as giving a vague recommendation, omitting relevant comp performance evidence or expert guidance, failing to provide confidence, citing evidence unrelated to the action, making an unsupported causal claim, or failing to stop when evidence is insufficient—the test fails. For each test, I will record the output, cited evidence, confidence level, pass or fail result, and the exact expected-result item missed in any failure.
