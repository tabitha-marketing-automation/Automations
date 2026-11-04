# Founder thought leadership engine (LinkedIn)

A weekly content routine that turns a founder's raw thoughts into reviewed, scheduled LinkedIn posts. The founder only does three things: add raw thoughts, review, approve.

**Stack:** Notion (inputs, review, approval) → Make (orchestration) → Claude (write, fact check, edit) → Buffer (scheduling)

## Weekly routine

1. **Monday:** the founder adds about 7 raw thoughts to the Content pipeline in Notion, one page each, and sets a **Publish date** on each.
2. When the thoughts are in, the founder changes each page's Status to **Create content**.
3. Claude writes the post, fact-checks it, and moves the page to **Ready for review** with the result in **Final draft**.
4. The founder reviews:
   - Happy → Status **Approved**. The post is scheduled on Buffer for the Publish date and the Status becomes **Scheduled**.
   - Not happy → writes what to change in **Edit brief**, sets Status **Not approved - edit**. Claude edits as per the brief, fact-checks again, and returns it to **Ready for review**.

Statuses: Raw thought → Create content → Ready for review → Approved → Scheduled. Loop: Ready for review → Not approved - edit → Ready for review.

## Make scenarios

1. **Create and edit content** (`make-scenario-create-and-edit.blueprint.json`): watch the Notion database, filter Status = Create content or Not approved - edit → read the page body and the Rules page → Claude writes the post (or edits the current draft per the Edit brief) → Claude fact-checks against the raw thought and Rules → write Final draft, Fact-check report, Fact check result → Status = Ready for review.
2. **Approved to Buffer** (`make-scenario-approved-to-buffer.blueprint.json`): filter Status = Approved → Buffer create status (LinkedIn profile, scheduled for the Publish date) → Status = Scheduled, store the Buffer post ID.

## Restrictions built into the prompts

No client or company names, no revenue, pricing or fundraising figures unless the founder marks them shareable, no names or emails in screenshots, nothing under NDA, no invented numbers. The full list, plus the dos and don'ts and the AI-phrase checklist, lives on the Rules page in Notion, which Claude reads on every run.

## What the fact check does

Every number, name and claim in the draft must be traceable to the founder's raw thought. Sensitive details are removed, AI-sounding phrases are stripped, and invented results are cut. The report of what was changed is saved on the page. If something cannot be verified, the result is "Needs founder input".

## Tested

The create and edit loop was tested end to end on an example row (Create content → Ready for review → Not approved - edit → Ready for review). The Buffer scenario is built but not run against the live LinkedIn queue, to avoid scheduling a test post.

## Honest limits

Text only: no images or video. Fact checking only verifies against what the founder supplied, not the wider web. Notion text fields hold about 2,000 characters, so posts are capped at 1,900. The Make trigger polls every 15 minutes, so a status change is picked up within that window.
