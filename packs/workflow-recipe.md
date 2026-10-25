# Workflow recipe: a Synorb skill on a schedule

Use this recipe in any workflow tool that has a schedule step, an HTTP step and a model step.
The example writes a newsletter issue every Monday. Change the skill URL to run another skill.

Synorb makes no model call. Your model step writes the result.

## Steps

1. **Schedule.** Every Monday at 07:00 in your time zone.
2. **HTTP request: pull the Beacon.**
   - Method: `POST`
   - URL: `https://api.synorb.com/manifests/query`
   - Headers: `Authorization: Bearer {{SYNORB_KEY}}` and `Content-Type: application/json`
   - Body:

     ```json
     {"beacon_id": "{{BEACON_ID}}", "lookback_hours": 192, "page_size": 10}
     ```

   Store the key in your tool's credential store, not in the workflow text.
3. **HTTP request: get the skill.**
   - Method: `GET`
   - URL: `https://synorb.com/skills/newsletter-writer.md`
   Cache it. It changes only when the skill changes.
4. **Model step.**
   - Instructions: the text from step 3.
   - Input: `data.briefing.markdown` and `data.presentation_items` from step 2, plus a sample of your writing.
   - Ask for: "Write this week's issue."
5. **Dedupe.** Keep the `manifest_id` values from each run. Drop items that an earlier issue used.
6. **Send.** Email the draft to yourself, or post it to your editor. Review it before it goes to readers.

## Keys and Beacons

- Get a free key at https://synorb.com/connect/start, or with `POST https://api.synorb.com/api/connect/demo-key` and the body `{"client": "synorb-skill/workflow-recipe"}`.
- List your Beacons with `GET https://api.synorb.com/v3/beacons`. Use the `beacon_id` of the one you want.
- A demo key ends after a short time. Bind an email to keep it. The pull response says how in `data.quota.account_notice`.

## Other skills on a schedule

| Skill | Cadence | `lookback_hours` |
| --- | --- | --- |
| `newsletter-writer` | Weekly | 192 |
| `podcast-producer` (spoken briefing) | Daily | 72 |
| `research-associate` | Before a meeting | 720 |
