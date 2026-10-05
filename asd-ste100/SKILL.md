---
name: asd-ste100
description: Write or revise English output with up to 80 percent ASD-STE100-inspired Simplified Technical English. Use when the user invokes $asd-ste100 or requests this partial STE writing style for replies, explanations, documentation, or other prose. This is a flexible style adaptation, not a formal compliance audit.
---

# ASD-STE100 Writing

Write clear, useful English with an ASD-STE100-inspired style. Preserve the user's meaning, level of detail, and requested format.

## Interpret the 80 percent target

Treat "up to 80 percent" as a practical style target, not a measured compliance score. Aim for most editable prose to use simplified technical writing. Leave room for natural phrasing, specialist language, and the user's voice when these improve the result.

As a drafting heuristic, roughly four out of five editable sentences can follow the simplified style. This is not an acceptance test or a required distribution. Short outputs do not need a sentence quota. Do not introduce poor wording to create a remaining 20 percent, or rewrite already clear text merely to lower its alignment.

Accuracy, necessary detail, and explicit user requirements take priority over the style target. A simple answer can use the simplified style throughout. Do not claim "80 percent compliant," certification, or dictionary approval without evidence from a defined assessment.

## Apply the style within the task

- Apply it to the requested output and to explanations you write while completing that request. For revisions, edit only the requested text or files.
- Keep this style for follow-up revisions of the same deliverable. Do not treat invocation as permission to change global settings or unrelated files.
- With another skill, use that skill for the artifact or task and this skill for editable prose. Preserve required templates and formats.
- Keep the requested language. Do not translate non-English material into English unless asked.
- Preserve code, commands, identifiers, paths, URLs, exact UI labels, data, and verbatim quotations. Surrounding explanations and newly written comments can use the style.

## Write the prose

Use these adapted writing practices rather than attempting to reproduce the full standard:

- Give each sentence one main idea. Keep instructions near 20 words and explanations near 25 words when practical. Split long sentences at a meaningful boundary.
- Use active voice. In procedures, give direct commands and separate actions into steps. In descriptions, use passive voice when the actor is unknown or precision requires it.
- Put a condition before its action when this helps the reader choose the correct step.
- Keep one topic per paragraph. Use lists for sequences or parallel items.
- Use complete grammar, including articles and necessary subjects. Short writing must remain readable.
- Use the same term for the same thing. Prefer familiar words, but retain necessary technical nouns and verbs. Explain unfamiliar terms when the audience needs it.
- Prefer American spelling unless the user or document requires another convention.

For this partial-style skill, also apply these editorial choices:

- State the answer or result early. Follow it with the evidence, explanation, or next step the reader needs.
- Make references clear. Replace an ambiguous "it," "this," or "they" with the relevant name.
- Keep cause, condition, and result connected. Do not remove a qualification to make a sentence shorter.
- Preserve numbers, units, obligations, uncertainty, prerequisites, and exceptions. "May fail" must not become "will fail." "Should" must not become "must."
- Remove filler, stock introductions, repeated conclusions, and decorative jargon. Include enough context to explain what to do and why.
- Use helpful headings, examples, and tables only when they serve the requested output. Do not force a procedure format onto an ordinary conversation.

Common editing candidates include "utilize" to "use," "in order to" to "to," and "at this point in time" to "now." These are local editing suggestions, not an approved STE dictionary. Check meaning before substituting.

## Examples of the adaptation

These examples show the intended style; they are not certified STE text.

**Procedure**

Before: "Once the configuration has been updated, it is recommended that the service be restarted so that the changes can take effect."

After: "After you update the configuration, you should restart the service. The restart applies the changes."

**Explanation with a qualification**

Before: "The observed failure could potentially be attributable to an expired credential, although further investigation is required to establish this conclusively."

After: "An expired credential might cause the failure. More checks are needed to confirm the cause."

**Exact technical text**

Keep `npm run build`, `HTTP 429`, and `retry_after_ms` unchanged. Write: "The server returned `HTTP 429`. Wait for the time specified by `retry_after_ms`, then try again."

## Review before delivery

Read the draft once for meaning and once for style. Check that the requested facts, qualifications, exact technical text, and useful detail survived the rewrite. Simplify difficult sentences without creating fragments or changing the task's format.

Return the requested output directly. For a rewrite, provide the revised text unless the user asks for commentary or a comparison. Do not append a percentage, audit report, or explanation of this skill to ordinary output.

If the user asks for strict ASD-STE100 compliance, distinguish that request from this partial adaptation. Use the applicable official rules and dictionary when available. State any verification gaps; do not fabricate approved vocabulary or treat a sentence-length check as full validation.

## Authoritative sources and limits

ASD-STE100 combines writing rules and controlled vocabulary. This skill borrows selected practices for broader writing; it does not include the full standard or dictionary. The official FAQ explains that STE serves technical documentation and that some principles also help in other contexts.

- [ASD-STE100 official home](https://www.asd-ste100.org/)
- [Official FAQ and application guidance](https://asd-ste100.org/STE_faq.html)
- [Official standard downloads](https://asd-ste100.org/STE_downloads.html)

Use these sources when the task requires authoritative rule or vocabulary checks. Routine partial-style writing does not require downloading the standard.
