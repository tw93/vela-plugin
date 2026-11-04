---
name: launch-posts
description: Use when the user wants to write launch posts by following the project's launch plan, one step at a time; drafts each post against the step's rule card (playbook), leaves steps without a rule card to the user, and routes to a different skill when the rule card forbids AI-generated text.
license: Proprietary. See LICENSE
---

## When to use

Use this skill when the user wants to write launch posts by following the project's launch plan, one step at a time, with a Vela rule card (playbook) guiding each post.

If the applicable rule card has ai_text_policy forbidden, switch to `fact-pack` for that step instead of drafting here.

If a tool reports that project_id is missing, follow its fix: call `list_projects` to get the id, or `create_project` when the account has no project yet.

## Tool sequence

1. `get_launch_plan` — read the plan with response_format detailed, which adds each step's playbook_ids and pending_cards; call `create_launch_plan` only when the project has no plan yet. When the chosen step's playbook_ids is empty (pending_cards lists the rule cards still missing), do not draft or check anything: tell the user that the rule card is pending and the step is theirs to handle, and call `complete_launch_step` once the user confirms it is done.
2. `get_playbook` — look up the rule card for the step; the step's playbook_ids show which communities the step covers. For each, pass the community site as platform (such as reddit) and the target board as venue (such as r/SaaS; leave venue out on sites without boards), and Vela returns the rule card that applies there.
3. `get_account_health` — check the account's posting rhythm before drafting; take the account profile id from `list_platform_accounts`, or call `save_platform_account` first when the account has no profile yet.
4. `get_draft_references` — before drafting, get the draft references: pass the rule card id from `get_playbook` as playbook_id, and opportunity_id when the post answers an opportunity. Vela returns this project's posts that brought visits to the site, saved quotes, product facts and example links, each with why it was selected. Use them only as reference and do not copy them: Vela does not write the draft, and the text is written by the user or by you.
5. Draft the post yourself, following the rule card's rules.
6. `check_draft` — revise the draft until it reports no fail, reusing the id returned by the first call; tell the user about any warn items. Do not pass playbook_id: Vela applies the rule card for the account profile's community site and board. Pass it only when the user wants one of their own child cards; if that returns invalid_input, do what its fix says. When `check_draft` returns a utm that is not null, add them as utm_source, utm_medium, utm_campaign and utm_content query parameters to the project link already in the text (the values stay the same on every check, so a link that already carries them needs nothing more), then run `check_draft` again with the same draft_id before the user publishes. When utm is null or the text has no project link, do not add a link for it.
7. Paste the finished post into the community yourself and publish it.
8. `register_post` — register the link of the published post and pass the draft_id returned by `check_draft`. If the post went out a while before it is registered (a late registration), also pass posted_at: the time it actually went out, in UTC ending in Z.
9. `complete_launch_step` — mark the step done once the post is published.

## Hard rules

Vela never posts on your behalf. Always paste the final text into the community yourself before publishing.

Keep revising with `check_draft` until it reports no fail before treating a post as ready; never tell the user to publish a draft that still has an open fail.

If the user says the community's rules have changed, report it with `log_rule_feedback`; do not edit the rule card yourself.

Only call the Vela tools named in this skill; do not invent additional Vela tool calls.
