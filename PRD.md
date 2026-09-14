# Product Requirements Document: Occasion Guide

**Status:** MVP direction 1.0
**Product:** Occasion Guide
**Release posture:** A simple, public, HTML-first information hub. Make the guide genuinely useful and easy to read before adding accounts, community features, or monetization.

## 1. Product idea

Occasion Guide helps a reader understand and prepare for a festival, family milestone, birthday, or celebration. It answers the practical questions a first-time reader has in one calm, structured place:

- What is this occasion?
- Why do people observe it?
- What should I prepare?
- What usually happens on the day?
- What might differ in my region or family?
- What should I confirm locally?

The site is an editorial reference, not an authority that declares one universal way to celebrate.

## 2. MVP audience and promise

The primary reader may be young, busy, away from home, or participating for the first time. They should be able to scan the page, understand the occasion, and leave with a practical next step in under five minutes.

**Promise:** Understand the occasion. Prepare what matters. Follow it with confidence.

## 3. MVP scope

### In scope

- One responsive static HTML page.
- A clear home/landing experience with a short explanation of the product.
- A small set of representative guides, presented as readable cards and sections.
- Search by title, alternate name, region, or keyword using lightweight browser JavaScript.
- Browse filters for festivals, family milestones, and celebrations.
- A consistent guide structure: at a glance, meaning, before, on the day, after, variations, local questions, safety/accessibility, and sources.
- A visible “start here” path for readers who do not know the terminology.
- Shareable section anchors and normal links; no account is required.
- Plain, respectful language that distinguishes common practice from local variation.

### Initial guide set

Start with a deliberately small catalogue:

- Bach Baras / Govatsa Dwadashi — regional festival example.
- Ganesh Chaturthi — home festival example.
- Jadula / Jat Jadula — family milestone example that requires local confirmation.
- Birthday gathering — secular planning example.
- Hosting at home — practical planning basics.

The collection should grow only when each guide has been reviewed, sourced, and filled using the same template.

### Explicitly deferred

- Sign-in, comments, community submissions, and moderation.
- Database, CMS, dashboards, reminders, saved guides, and personalised calendars.
- Vendor listings, affiliate links, paid listings, sponsorship placements, and checkout.
- Medical, astrological, legal, or mandatory ritual advice.
- Full translations and automatic date calculation.

## 4. Core reading experience

The page follows one predictable path:

1. **Start here:** search or browse a guide.
2. **At a glance:** name, alternate names, audience, and short summary.
3. **Understand it:** neutral meaning and context.
4. **Prepare:** the three-part Preparation Path — Before, On the day, After.
5. **Adapt it:** what may vary by region, community, place of worship, or family.
6. **Confirm locally:** questions to ask an elder, organiser, priest, or place of worship.
7. **Trust the page:** sources, review date, and correction contact/placeholder.

The visual language should match `cimulink-vsl-manufacturing`: warm paper background, pine panels, slab-serif headlines, mono utility labels, structured grids, sharp borders, and restrained motion. Occasion Guide may feel warmer through sand/clay accents and generous reading space, but it should still look like the same Cimulink family.

## 5. Content rules

- Use “many families,” “in some regions,” and “you may see” when practice is not universal.
- Put practical preparation before long background.
- Label sourced editorial context separately from future community notes.
- Never describe a material, fast, date, donation, food, or ritual action as universally required without a clearly bounded source and context.
- Include a safety/accessibility note where food, children, fire, crowds, travel, or physical participation may matter.
- Every guide shows its source links and review date.
- Every guide offers a way to flag a correction, even if the first implementation uses a simple email link.

## 6. Success criteria for the MVP

- A reader can find a relevant guide from the landing page without signing in.
- A reader can answer “what is it?”, “what do I prepare?”, and “what may vary?” after reading a guide.
- The page remains usable on a 320 px-wide screen and with keyboard navigation.
- The catalogue can be expanded by adding structured HTML data without changing the layout.
- Five to ten readers from different backgrounds describe the guide as clear, respectful, and practically useful.

## 7. Later business model direction

First earn trust through useful, transparent information. Later, test monetization around optional value rather than withholding basic understanding:

- printable/shareable checklists;
- carefully reviewed preparation bundles or partner resources;
- sponsored seasonal collections with clear labelling;
- premium planning/reminder tools for families and organisers.

No monetization is part of the MVP, and no commercial placement should influence editorial guidance.

## 8. Decisions still needed later

- Public product name and domain.
- Editorial reviewer and correction owner.
- Which regions/languages deserve the next guide slots.
- Whether future contributions use real names, display names, or initials.
- Which monetization experiment best fits reader trust after usage evidence exists.
