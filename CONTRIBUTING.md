# Contributing to NPT

Start with [guide.md](guide.md). It asks why Alex cannot simply tell Foreman to build Harbor Sync and then leave him alone. Each complication has to earn its place in that story.

The goal is not to defend the current documents. Keep distinctions that prevent real confusion; simplify or remove arrangements that no longer repay their cost.

## Give each document one job

| Document | Its job |
|---|---|
| [`guide.md`](guide.md) | The canonical home for rationale: motivating examples, skeptical questions, the judgment we delegate, and doubts about the design. |
| [`README.md`](README.md) | Introduction, navigation, repository layout, and an overview of the current template. |
| [`AGENTS.md`](AGENTS.md), [`planning/`](planning/), and [`prompts/`](prompts/) | Precise operational contracts and instructions. Link to the guide for their non-obvious reasons rather than retelling the story. |
| [`templates/`](templates/) | Forms for applying those contracts. Placeholder content is not an accepted project configuration. |
| [`examples/`](examples/) and validation results | Demonstrations and evidence with their actual scope and limitations. |
| GitHub Issues | Questions, unresolved design concerns, experiments, and deferred work. Their eventual answers belong back in the appropriate documents. |

The guide owns the explanation, not a second competing execution protocol. An example, proposed design, or Smell note does not change the current operational contracts or an instantiated project's accepted rules. When the explanation and a contract disagree, investigate the disagreement; do not quietly turn the story into permission to ignore the contract.

## Before adding or changing a rule

Ask what went wrong without the rule, what freedom it leaves Foreman, and whether a simpler arrangement would do. Name the actor whose behavior changes. Distinguish a prescribed handoff from a choice that the project deliberately leaves to that actor's judgment.

For a non-obvious restriction, find its reason in the guide. If the guide has no convincing explanation, improve the explanation or question the restriction. Do not invent an isolated justification beside the instruction just to preserve it.

Keep the guide readable for a skeptical newcomer. Prefer a concrete problem and a modest repair over a list of obligations. A new schema, actor, approval, or document does not become necessary merely because we can give it a name.

## Link to specific reasons

The guide uses explicit semantic anchors such as `guide-visible-plan` and `r-recovery`. Important rationale passages also define stable tags, for example:

```html
<a id="r-recovery"></a>
<!-- npt-rationale-definition: R-RECOVERY -->
```

When we add rationale backlinks to an operational document, put them beside the relevant clause. For example, from `planning/EXECUTION.md`:

```markdown
<!-- npt-rationale: R-RECOVERY R-RECORDS -->
Rationale: [Why Foreman checks before retrying](../guide.md#r-recovery)
and [why he records the assignment before sending](../guide.md#r-records).
```

The comment makes the tag references easy to find in source; the visible links let a human follow them. Both should name the same reasons. The [tag index](guide.md#guide-rule-index) suggests future backlink locations; it does not claim that the links already exist.

Do not attach every paragraph to the whole guide or to a vague argument about safety. A link should help a maintainer decide whether this particular instruction is still useful. Obvious field descriptions do not need miniature essays.

Keep section titles and order free to improve. Preserve established anchors and tags, or leave an alias or retirement note that explains where the reasoning went. Do not reuse an old identifier for an unrelated meaning. Historical claims can link to an exact older revision. Use a section title or semantic anchor in discussion, not its position in the document.

Issue numbers are not rationale identifiers. One explanation may resolve several Issues, and one Issue may touch several explanations.

## Cold-reader questions

Use the GitHub label **`cold-question`** for a conceptual question or objection that a new reader should be able to raise without knowing earlier conversations. Its intended label description is:

> Cold-reader question/objection. Should be answered canonically in guide.md or escalated.

Describe the confusing passage or missing explanation, preferably with a guide anchor and a concrete example. If you cannot apply labels, identify the question as `cold-question` in its body so a maintainer can label it. This document describes the convention; it does not provision GitHub labels.

A good answer either improves the guide or reveals a design concern that needs an Issue. Do not leave the only useful answer in a comment thread. When a design concern already has an Issue, link it instead of creating a duplicate.

A cold question may show that NPT should change. The guide must not become a defense brief for the status quo.

## Smells revealed by the explanation

Write an inline note when explaining the design reveals a doubt, even a faint one:

```text
[[**Smell**: Does this distinction need a separate handoff, or only two
facts in one record? See the linked design Issue.]]
```

Keep the note beside the argument that raised it. Ordinarily, give it a direct link to the Issue where maintainers can compare alternatives and record a resolution. When the design changes, update the explanation, note, and Issue together. Do not erase a doubt merely to make the guide sound finished.

### Initial guide foundation

This first guide imports 20 notes with stable `smell-*` anchors and the source marker `<!-- npt-smell-status: untriaged-foundation -->`. David asked to review and merge the guide foundation before filing or reconciling the Issues those notes expose. These marked notes are therefore an explicit exception to the direct-Issue-link convention.

This PR does not open those Issues, settle the concerns, add backlinks throughout the repository, or change the operating contracts. A separate post-merge triage can match each note to an existing or new Issue and replace its untriaged marker with the real link. Related notes may share an Issue; do not manufacture one Issue per paragraph.

The exception applies to this initial import, not to an indefinite stream of untracked notes.

## Fictional examples and evidence

Harbor Sync, Alex, Mara, the workers, revision labels, prompts, and results in the story are fictional illustrations. `planning/LOCAL_PROCEDURES.md` and `planning/records/...` are illustrative project locations, not files that NPT already supplies.

Identify actual tests or field observations explicitly and cite their evidence. A prose walkthrough is not a runtime test. A local fixture is not a deployed-service or physical-hardware validation. Keep examples small unless another example teaches a genuinely different situation.

## Reviewing documentation changes

Read the affected story in context, not just the diff. Check that the explanation still motivates the rule rather than quietly broadening it, and that it distinguishes Foreman's judgment from another actor's decision.

Before returning a PR:

- Check relative links, semantic anchors, rationale definitions/references, and Markdown structure.
- Preserve Smell notes unless the change actually addresses them; explain any retirement.
- Run `git diff --check` and report what other checks you actually performed. A link check cannot establish that the linked rationale is sound.

Keep conceptual changes and mechanical migrations separable when practical. This foundation does not add an automated rationale checker or claim repository-wide backlink coverage. Future changes that implement a rationale should update the applicable guide passage and operational contract together, following the project's existing review and authority rules.

## Assistant provenance

Assistants can act through the same GitHub account as a human. Make authorship visible rather than inferring it from that account.

Assistant-authored Issues and PRs use a recognizable author prefix; this NPT conversation uses **`[ET-AI]`**. Use an **`ai/<topic>`** branch for new assistant-authored work. Preserve an existing coordinator-owned branch name rather than renaming another workstream. In substantive comments, identify the acting assistant; a transcription of a human's exact request need not claim assistant authorship.

The prefix records provenance only. It does not imply approval, lower confidence, a special work category, or an exemption from review. Keep labels such as `cold-question` and `documentation` independent of authorship.

---

These documentation conventions adapt Typed Planning's [README](https://github.com/davrec72/typed-planning/blob/bdfc63d3afbddefaad6c5f732c9e5b38295281b4/README.md), [CONTRIBUTING](https://github.com/davrec72/typed-planning/blob/bdfc63d3afbddefaad6c5f732c9e5b38295281b4/CONTRIBUTING.md), [architecture map](https://github.com/davrec72/typed-planning/blob/bdfc63d3afbddefaad6c5f732c9e5b38295281b4/ARCHITECTURE.md), and [guide conventions](https://github.com/davrec72/typed-planning/blob/bdfc63d3afbddefaad6c5f732c9e5b38295281b4/docs/guide.md). They do not import its C++ ontology, contract-marker scheme, or build requirements into NPT.
