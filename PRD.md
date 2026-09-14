# Product Requirements Document: Occasion Guide

**Status:** Draft 1.0  
**Product:** Occasion Guide  
**Audience:** People preparing for a festival, family milestone, birthday, or celebration who want a clear, respectful answer to “what do we do, why do we do it, and what should I prepare?”

## 1. Product summary

Occasion Guide is a calm, practical website for celebrations that are important but often confusing to plan. It combines a simple guide, a preparation checklist, regional and family variations, and moderated discussion.

The product must not position one ritual as the only correct version. A person in Jaipur preparing for Bach Baras, a family planning a child's Jadula, someone celebrating Christmas, or a parent organising a birthday should be able to start with what they know, see what commonly varies, and ask a respectful question.

## 2. The problem

People often search in fragments:

- “What do we do for Bach Baras?”
- “What should we take for my baby's Jadula?”
- “What is needed for Ganesh Chaturthi at home?”
- “How do we celebrate Christmas with children?”

Search results can be repetitive, commercial, too prescriptive, or silent about regional variation. Families then rely on multiple calls, WhatsApp messages, and memory. The result is unnecessary anxiety around an occasion meant to feel meaningful.

## 3. Product promise

**Understand the occasion. Prepare what matters. Ask with confidence.**

Every guide gives the visitor four answers in under five minutes:

1. What is this occasion and why do people observe it?
2. What do families commonly prepare?
3. Which parts may differ by region, community, temple, church, or family?
4. What should I confirm with my own elder, priest, organiser, or place of worship?

## 4. Goals and non-goals

### Goals

- Make occasion guidance simple enough for a first-time participant.
- Preserve regional, linguistic, religious, and family variation instead of flattening it.
- Give people usable checklists, planning timelines, and respectful discussion.
- Build an editorial base that can cover both religious and secular occasions.
- Let members add context and questions without allowing misinformation, mockery, or commercial spam to dominate the page.

### Non-goals for v1

- Replacing a priest, religious leader, elder, doctor, caterer, or event planner.
- Giving mandatory ritual instructions, astrological advice, legal advice, or medical advice.
- Selling puja materials, gifts, travel, or vendors.
- Hosting real-time chat, direct messages, or unmoderated anonymous comments.
- Trying to cover every faith, region, and occasion at launch.

## 5. Audience and jobs to be done

| Person | Situation | Job to be done |
| --- | --- | --- |
| First-time organiser | A festival or baby ceremony is approaching | “Give me a simple starting point and a list I can share with family.” |
| Young adult living away from home | Wants to participate respectfully | “Explain the meaning and what I should ask my family.” |
| Parent or relative | Planning a birthday, Jadula, naming ceremony, or family gathering | “Help me prepare calmly, with room for our family tradition.” |
| Community contributor | Knows a regional practice | “Add context without arguing that my way is the only way.” |
| Returning visitor | Tracks multiple occasions in a year | “Save, revisit, and plan the next celebration.” |

## 6. Launch scope

### Seed occasion collection

The first collection should prioritise depth over a large catalogue.

| Collection | Initial guides |
| --- | --- |
| Hindu festivals | Bach Baras / Govatsa Dwadashi, Ganesh Chaturthi, Holi, Diwali, Raksha Bandhan, Janmashtami, Navratri, Makar Sankranti |
| Christian celebrations | Christmas, Good Friday, Easter |
| Family milestones | Birthday, first birthday, naming ceremony, Mundan / Chudakarana, Jadula / Jat Jadula where regionally relevant |
| Planning basics | Hosting at home, inviting family, food preferences, inclusive participation, low-waste celebrations |

The first Bach Baras guide should be explicitly tagged as regionally varied; the Ministry of Tourism describes it as a significant Rajasthan observance associated with the well-being of calves. Jadula should be introduced as a regional baby hair-cut ceremony variant and require local/family verification before publishing step-by-step guidance. See [research notes](#14-editorial-research-and-sourcing).

## 7. Core user experience

### Home page

The home page is a calm seasonal guide, not a dense directory.

1. **Today / coming up:** current and upcoming occasions, with date context where editorially verified.
2. **Start with your question:** search such as “What do I need for a Ganesh Chaturthi at home?”
3. **Browse by life moment:** festivals, baby and family, birthdays, faith traditions, and hosting.
4. **Regional lens:** choose a state, language, or “show variations.”
5. **Ask the community:** a safe, moderated path to a specific question.

### Occasion page

One page must feel like one clear path, in this order:

1. **At a glance:** name, alternate names, timing, and a plain-language summary.
2. **Why people observe it:** short, neutral context with sources.
3. **A simple way to prepare:** a checklist grouped by before / on the day / after.
4. **What may vary:** region, language, denomination, community, household, temple/church, dietary choice, and personal preference.
5. **Ask your family or local guide:** questions the reader can take to an elder or religious leader.
6. **Community notes:** approved, contextual comments and questions.
7. **Related occasions:** only genuinely connected guides.

### Comment and question flow

1. Reader selects “Ask a question” or “Share a regional variation.”
2. They sign in and choose a contribution type: question, regional note, family variation, accessibility tip, or correction request.
3. The form asks for region/language only when relevant and makes it optional.
4. Contributions enter a moderation queue before public display.
5. Approved contributions appear in a flat thread with reporting and helpfulness controls.

## 8. Content template

Every occasion guide uses the same editorial skeleton.

```text
Title and alternate names
When it occurs
In simple words
Why people observe it
Common preparations
On-the-day flow
What changes by region or family
Questions to confirm locally
Accessibility, safety, and low-waste notes
Sources and editorial review date
Community notes
```

### Editorial rules

- Use “many families,” “in some regions,” and “you may see” when practice varies.
- Separate source-backed context from community-contributed context.
- Never require fasting, a material, a donation, an astrological date, or a ritual action as universally necessary.
- Do not publish casteist, gender-discriminatory, exclusionary, or coercive instructions.
- Do not publish medical claims about rituals, pregnancy, babies, food, or fasting.
- Provide a visible correction route on every page.

## 9. Design direction

Carry forward the VSL's calm editorial system, but make it warmer and more domestic:

- **Pine `#164B43`:** trust, navigation, and primary actions.
- **Warm paper `#F5F4EE` / off-white `#FFFEFA`:** long-form reading comfort.
- **Moss `#86A967`:** seasonal and practical markers.
- **Sand `#E9DFCC`:** preparation cards and gentle visual pauses.
- **Clay `#C56848`:** important dates, reminders, and corrections.
- **Typography:** one readable display face for page titles, one body face, and one small utility label; do not compete with the guide itself.

The signature interface element is a **Preparation Path**: three quiet cards - “Before”, “On the day”, and “After” - that turn a cultural guide into a reassuring plan. Images should show objects, food, materials, and atmosphere rather than treating people or rituals as decoration.

## 10. Functional requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| FR-01 | Visitors can browse, search, and read all published guides without an account. | Must |
| FR-02 | Each guide supports alternate names, tags, regions, source links, review date, and related guides. | Must |
| FR-03 | Each guide contains the standard content template and a preparation checklist. | Must |
| FR-04 | Visitors can submit a question, regional note, correction, or accessibility tip after sign-in. | Must |
| FR-05 | No contribution becomes public until a moderator approves it. | Must |
| FR-06 | Members can report an approved comment. | Must |
| FR-07 | Editors can publish a correction note and retain an internal edit history. | Must |
| FR-08 | Visitors can filter by occasion type, month/season, region, and faith/tradition where supplied. | Should |
| FR-09 | Members can save guides and receive optional seasonal reminders. | Later |
| FR-10 | Guides support English first, then Hindi and regional-language translations with reviewer attribution. | Later |

## 11. Success measures

### Early product signals

- At least 70% of tested visitors can find a relevant guide within two minutes.
- At least 80% can answer “what should I prepare?” after reading an occasion page.
- At least 60% describe the guide as respectful of family/regional variation.
- Fewer than 10% of submitted comments need rejection for safety or relevance after contributor guidance is improved.

### Operational signals

- Median moderation time under 24 hours.
- Every published guide has at least two appropriate sources or an explicit “community-sourced; needs review” label.
- Every factual correction is acknowledged or resolved within seven days.

## 12. Release plan

### Phase 0 - Editorial prototype

- 8-12 well-reviewed seed guides.
- Static pages, no accounts or public comments.
- Validate reading flow and content template with families from different regions.

### Phase 1 - Guided participation

- Sign-in, comment submission, moderation queue, reporting, and editor tools.
- Search, filters, and source/review labels.

### Phase 2 - Personal planning

- Saved guides, optional reminders, shareable checklists, and regional-language expansion.

## 13. Risks and decisions

| Risk | Product decision |
| --- | --- |
| A guide is mistaken for a universal rule | Put “what may vary” near the top and show sources/review date. |
| Comments become sectarian, abusive, or commercially spammy | Require sign-in, pre-moderate, rate-limit, report, and keep flat threads in v1. |
| A date or ritual detail is wrong | Store source and review metadata; publish correction notes; do not infer dates from a generic calendar. |
| Content feels too academic | Lead with practical preparation; keep sources available without interrupting the main path. |
| Content feels commercially exploitative | No vendor marketplace or affiliate links in v1. |

## 14. Editorial research and sourcing

The content team needs a source hierarchy:

1. Official cultural institutions, museums, government heritage/tourism sources, and recognised places of worship when they describe their own observance.
2. Scholarly and reputable cultural publications.
3. Named regional/community contributors, clearly labelled as their experience.
4. Never use an unverified social post as the sole basis for an instructional claim.

Initial planning references:

- The Government of India's [Utsav festival entry for Bach Baras](https://utsav.gov.in/view-event/bach-baras-1) identifies it as a Rajasthan observance connected to calf well-being.
- The Ministry of Culture's [Vedic Heritage Portal](https://culture.gov.in/sanskriti/vedic-heritage-portal) is an example of an institutional source type for sacred-text context; it does not replace local guidance.
- The [Sangeet Natak Akademi intangible cultural heritage collection](https://sangeetnatak.gov.in/sections/ICH) demonstrates the regional specificity of rituals and festive events.

## 15. Open questions

- What should the public product name and primary domain be?
- Which regions and languages should guide the first 12 articles?
- Who has editorial authority to approve religious and regional content?
- Should members use their real names, a display name, or only initials?
- What is the initial age policy for accounts and comments?
- Should the first release include Christian occasions, or should it launch as an India-first festival and family-milestone guide before broadening?

