# Founder thought leadership engine (LinkedIn)

A content calendar that turns a founder's raw thoughts into reviewed LinkedIn posts. The founder does two things: drops in raw thoughts, and approves the final draft. Everything between is automated.

**Stack:** Notion (inputs, review, approval) → Make (orchestration) → Claude (draft, fact check) → Buffer (scheduling)

## Flow

| # | Status in Notion | Who | What happens |
|---|---|---|---|
| 1 | Raw thought | Founder | Adds a number, screenshot or client-call insight. Ticks "Contains sensitive info" if unsure |
| 2 | Drafting | Claude | Writes the post and a visual brief (image, carousel or short video) following the Rules page |
| 3 | Fact check | Claude | Second pass: checks every claim against the raw thought, removes sensitive details, strips AI phrases |
| 4 | Ready for review | Founder | Edits the final draft. Approves or sets "Changes needed" |
| 5 | Approved | Make | Sends the post to Buffer on the publish date |
| 6 | Sent to Buffer | Make | Stores the Buffer post ID |

## Make scenarios

1. **Draft:** watch Notion database, filter Status = Raw thought → set Drafting → Claude draft → write Draft post + Visual brief → set Fact check.
2. **Fact check:** filter Status = Fact check → Claude check against raw thought and Rules → write Fact-check report + Final draft → Fact check result Passed → Ready for review; otherwise Needs founder input + Changes needed.
3. **Publish:** filter Status = Approved and Publish date set → Buffer create status (LinkedIn profile, scheduled) → Status = Sent to Buffer, store Buffer post ID.

## Restrictions built into the prompts

No client or company names, no revenue, pricing or fundraising figures unless the founder marks them shareable, no names/emails in screenshots, nothing under NDA, no invented numbers. Full list lives on the Rules page in Notion, which Claude reads on every run.

## Claude prompts

**Draft (system):** You write LinkedIn posts for a founder. Use only facts, numbers and quotes from the raw thought. Never invent results. Remove anything in the restrictions list. First line under 12 words, one idea, 120-220 words, sentence case, max 3 hashtags, link goes in the first comment. Then write a visual brief: image, carousel or short video, no real client logos or names. Output JSON: {post, visual_type, visual_brief, removed_sensitive_items}.

**Fact check (system):** You are a strict editor. Compare the draft to the raw thought. List every claim not traceable to the raw thought. Remove or rewrite it. Remove any AI-sounding phrases from the checklist. Remove sensitive details. Output JSON: {result: PASS|NEEDS_FOUNDER_INPUT, issues[], final_draft}.

## Brand and visual guidelines

Each founder fills in a Brand and visual guidelines page in Notion once: colours (hex), fonts, layout and format, name line, logo rules, visual dos and don'ts, and content dos and don'ts. Claude reads it, together with the Rules page, before every post and every visual, and lists which guideline items it applied. The example in the template is the colour and font set of this portfolio (Brick Rust, Bone, Burnt Ink; Anton, Tinos Bold Italic, DM Sans; static title and static name line; no yellow).

Content dos: lead with the result, plain sentence-case words, only facts from the raw thought, link in the first comment. Content don'ts: no invented numbers, no client names, no AI phrases, no comment-keyword calls to action, max 3 hashtags.

Visual dos: real screenshots and numbers, highlight what to look at, one idea per visual, zoom in rather than leave empty space. Visual don'ts: no client data or faces, no stock or AI-generated people, no invented charts, no extra colours or fonts, no animated title.

## Visuals: Claude creates them too

Claude produces the finished visual, not just a brief: a branded image, a carousel, or a short animated video built from the founder's own screenshots and numbers. It writes the visual as code (HTML/SVG), which is rendered to a PNG or MP4 in the brand's colours and fonts. The title and the founder's name line stay static; only the screenshots or numbers animate.

Visual rules (same restrictions as the post): no client names or logos, no emails or personal data visible in screenshots, no confidential figures. Screenshots are cropped or blurred before use, and any that cannot be made safe are replaced by a redrawn version.

In the Make build, the visual step sends Claude's HTML to a render step and saves the file link back to the Notion row ("Visual file"), so the founder reviews the post and the visual together.

## Honest limits

Visuals are designed layouts, charts and screen-recording-style animations, not photorealistic AI-generated pictures. Fact checking only verifies against what the founder supplied, not the wider web.
