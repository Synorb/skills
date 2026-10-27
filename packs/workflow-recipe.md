# Workflow recipe: scheduled Synorb work

Use this pattern in a workflow tool that supports scheduled triggers, HTTP, a model step, and persistent state. Adapt the cadence and output to the user's request. Synorb supplies cited evidence; the user's model reasons, renders, and writes the result.

## Inputs to carry into every run

Keep a compact, user-controlled job brief with the decision or purpose, audience, priorities, constraints, expertise, desired depth, tone, and output format. Include only relevant details and distinguish stated preferences from tentative inferences. If no useful memory is available, say so internally and use the current request; do not invent a profile.

Also pass the prior assessment (conclusions, open questions, and what would change the view), the last successful delivery window, the IDs already delivered, and the capabilities actually available to the workflow (schedule, persistent state, delivery destination, visual renderer, audio tool). Keep private context out of public-facing material unless the user intends to publish it.

## Run sequence

1. **Recover the window.** Query the Beacon from the last successful checkpoint through the current run, with a small overlap to cover boundary delays. If one or more runs were missed, fetch the whole missed interval in bounded pages or date slices. Disclose any entitlement, pagination, or retrieval limit; never report a partial window as complete.
2. **Fetch evidence.** `POST https://api.synorb.com/manifests/query` with `Authorization: Bearer {{SYNORB_KEY}}`, `Content-Type: application/json`, and a body such as:

   ```json
   {"beacon_id":"{{BEACON_ID}}","lookback_hours":192,"page_size":5}
   ```

   Use only supported request fields. Check the returned quota and effective window. Keep the key in the workflow credential store, never in prompts, logs, or saved state.
3. **Prepare the model input.** Fetch and cache the selected skill from `https://synorb.com/skills/{{SKILL_NAME}}.md`. Pass the compact brief, prior assessment, returned cited evidence, prior delivered IDs, and the capability list. Keep only enough history to explain continuity.
4. **Dedupe before drafting.** Remove already-delivered `manifest_id` values before asking the model to write. Also identify repeated articles or substantially identical events when their source identity is clear. Revisit an old item only when a substantive update changes its meaning, and label it as an update. Do not draft first and filter afterward.
5. **Draft the useful job.** Ask the model to prioritize evidence for this user's purpose, explain material support and disagreement, update the prior assessment, and choose a length and format that fit the request. A quiet or empty result is valid; do not pad to a fixed item count.
6. **Use visuals only when supported and useful.** If the available renderer can produce and inspect an artifact, make a chart, timeline, diagram, or matrix only when it clarifies a real comparison, pattern, sequence, or relationship. Include cited source data, units, periods, caveats, and a text equivalent. If rendering or inspection is unavailable, provide prose or a table and state that plainly; do not claim an artifact was created.
7. **Deliver.** Send to the user-approved destination or save a draft for review. Do not add recipients or publish publicly without authorization. For a newsletter or other public copy, keep private rationale and personal details out unless intended for publication.
8. **Commit state only after delivery succeeds.** After the destination confirms success, atomically save the delivered IDs, concise assessment, open questions, successful window/checkpoint, and skill version. If delivery fails, preserve the previous checkpoint and retry or surface the failure; do not mark the items as delivered.

## Setup

- Obtain a key at `https://synorb.com/connect/start`, or request a demo key with `POST https://api.synorb.com/api/connect/demo-key` and `{"client":"synorb-skill/workflow-recipe"}`. Store it in the credential manager. A demo key is temporary; follow the account notice in the response.
- List Beacons with `GET https://api.synorb.com/v3/beacons`; select one that matches the requested coverage. Do not create or change a Beacon unless the user has authorized that action.
- Schedule only when the host actually supports scheduling. If it does not, explain that runs are manual and do not imply Synorb is watching or will send updates.

## Cadence examples

Choose a window long enough to cover the interval, plus overlap for recovery. These are starting points, not guarantees of complete coverage.

| Job | Example cadence | Example `lookback_hours` |
| --- | --- | ---: |
| `newsletter-writer` | Weekly | 192 |
| `podcast-producer` | Daily | 72 |
| `research-associate` | Before a meeting | 720 |
