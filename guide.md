# Why can't I just tell Foreman to do the whole project?

> “Foreman, make Harbor Sync for me. Tell me when it's done.”

That is how Alex would like to manage the project. He wants an application that uploads recordings from a phone. He does not want a second job supervising agents, arranging reviews, or maintaining a miniature bureaucracy.

Foreman can write code, commission other workers, investigate failures, and come back later. Why not give him the whole job?

**Sometimes that is enough.** For a small experiment, Alex may be happy to inspect the result and either keep it or ask for another attempt. A capable Foreman may also create a perfectly useful plan and working records without anyone mentioning NPT.

NPT therefore has something to prove. It should not make delegation harder merely to make it look more organized. It earns its place when a project needs other people to understand, question, or continue the work—and a private conversation with Foreman no longer gives them enough to do that.

<a id="r-proportion"></a>

<!-- npt-rationale-definition: R-PROPORTION -->
The story below starts without a planning system. Each time the project encounters a problem, Alex and Foreman try a small repair. Sometimes they need a shared document. Sometimes Foreman simply needs to make a better judgment. We should notice the difference.

*Harbor Sync, its people, prompts, and results are fictional. This guide is NPT's canonical home for design rationale, not a deployment procedure. It explains and questions the existing contracts; it does not replace them or make the story's local choices operative. The [source appendix](#guide-sources) distinguishes existing files from illustrative additions.*

<a id="smell-story-bias"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A story can make almost any design look inevitable by arranging convenient failures. The problems below motivate distinctions; they do not prove that NPT's present machinery is the cheapest way to preserve them. A simpler repair is a reason to change the design, not a failure to appreciate it.]]

<a id="guide-contents"></a>

## Follow the story

[Agree on the job](#guide-job) · [Expose the plan](#guide-visible-plan) · [Give others useful work](#guide-assignment) · [Find out whether it works](#guide-review) · [Improve the process](#guide-advice) · [Keep the project understandable](#guide-handoff) · [Maintain the reasons](#guide-links)

<a id="guide-job"></a>

<a id="guide-example"></a>

## Foreman delivers the wrong Harbor Sync

Foreman gets to work. He builds an uploader, a progress display, and automatic retries. To save space, he compresses videos before upload. To simplify the server, he gives each uploaded file a new timestamp.

A few days later, Alex opens the app. It works. Then he downloads a recording.

“This isn't the original file.”

Foreman explains the tradeoff. Smaller files upload faster, and the server's timestamps make sorting convenient.

“But these are my source recordings,” Alex says. “Preserving them is the point.”

Foreman has not betrayed Alex. He has filled in a decision that Alex never expressed. More intelligence might have prompted him to ask earlier, but it could not have made an unstated preference certain.

They could try a more emphatic instruction: “Build exactly what I mean.” That would leave the same problem underneath.

Instead, Foreman writes down what Alex now says:

> Harbor Sync uploads recordings without changing their bytes or original recording timestamps. Interrupted uploads can resume. The first release must work on an actual phone with an unreliable connection, not just in a desktop demonstration.

Alex reads that paragraph and changes one phrase. Now they have a promise they can both point to.

<a id="r-success"></a>

<!-- npt-rationale-definition: R-SUCCESS -->
The important improvement is not that Alex has constrained every implementation decision. He has made the destination visible. Foreman can still choose the interface, protocol, tools, and internal design. He can also recommend changing the promise, but he can no longer quietly substitute a more convenient one.

In NPT, [`planning/PLAN.md`][src-plan] gives this sort of promise a home in the outcome and acceptance criteria of a milestone. Harbor Sync can keep its broader purpose alongside those contracts. We have not yet earned a separate file or object for every sentence Alex cares about.

<a id="smell-changing-goals"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Alex may discover another important preference only after using the app. A written goal does not finish the conversation or make his first wording infallible. Does NPT make it easy to refine an honest misunderstanding, or does it encourage everyone to defend an obsolete contract because it is already “accepted”?]]

<a id="guide-visible-plan"></a>

## “What are you going to do next?”

Foreman removes the compression and fixes timestamp handling. The project improves. Alex asks when he can try it on his phone.

Foreman says Friday.

On Friday, the server looks excellent, but nobody has tried a disconnected phone. Foreman spent the week improving throughput. He thought the field trial would be easier after that.

Alex would have preferred a rough field test on Tuesday. A failure on a real phone could have changed the entire design. But he could not question an ordering decision that he never saw.

A more detailed status message would help a little. What Alex really needs is a view of **the work ahead**, while he can still influence it.

Foreman adds a short plan:

| Outcome | What would let us believe it? | What comes first? |
|---|---|---|
| M1: We can verify an unchanged recording | Compare source and received bytes and recording metadata | Nothing |
| M2: Uploads survive interruption and retry | Run the agreed interruption cases against the uploader and receiver | M1 |
| M3: The first release works in the field | Complete the agreed trial on an actual phone | M2 for the release decision |

Foreman also proposes an early phone experiment. It cannot establish M3 yet, but it can expose bad assumptions before the team invests much more work. Alex agrees.

That conversation changes the plan before it changes a large amount of code.

<a id="r-visibility"></a>

<!-- npt-rationale-definition: R-VISIBILITY -->
**An exposed plan makes delegation discussable.** Alex can question priorities without choosing function names. A worker can see why a task matters. A reviewer can see what the project intends to establish. A successor can see what remains open.

The plan is not a transcript of Foreman's thinking, and Alex does not need to approve every edit to a private sketch. It is the shared account of the commitments the team is actually following. Foreman proposes it; Alex agrees to the initial direction. Later, the project can delegate ordinary changes without hiding them.

This is the first point where a reusable planning convention begins to earn its keep. Everyone should know where that shared account lives and what its terms mean. NPT uses `planning/PLAN.md` for the roadmap and [`planning/CONVENTIONS.md`][src-conventions] for its vocabulary.

<a id="smell-unused-roadmap"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A polished roadmap can become another report that nobody works from. If Foreman maintains one plan in his head and a reassuring one in `PLAN.md`, we have added work without adding visibility. The guide should help us ask whether the shared plan actually influences assignments and decisions.]]

<a id="guide-judgment"></a>

## The plan should not take Foreman's job away

Alex now sees more of the work. He is pleased—until Foreman starts asking whether to investigate a failed retry before improving the progress display, whether to use a second worker, and whether to keep yesterday's useful implementation chat.

“I wanted to see the plan,” Alex says. “I didn't ask to become the scheduler.”

They have overcorrected. Visibility has become a request for permission at every turn.

<a id="r-judgment"></a>

<!-- npt-rationale-definition: R-JUDGMENT -->
Alex tells Foreman to make those ordinary choices himself. He gives him a working budget and room to choose priorities, workers, and extra investigation. Alex still wants to hear about changes to Harbor Sync's purpose, a larger spending commitment, or a serious unresolved risk.

Foreman chooses to investigate the retry failure first. Another good Foreman might have reproduced it in parallel with the interface work. Neither choice needs to appear in a prewritten decision tree.

The point of a plan is to help intelligent coordination, not to replace it with a sequence of approvals. [`prompts/FOREMAN.md`][src-foreman] describes the coordinating job; the project's own delegation says how much discretion the holder has. [`planning/EXECUTION.md`][src-execution] already allows a standing authorization to cover a bounded class of packages.

<a id="r-readiness"></a>

<!-- npt-rationale-definition: R-READINESS -->
There is still a difference between an ordering preference and a real dependency. Foreman can move interface work around. He cannot call M2 complete before the project can check whether an upload preserved its source.

That is why NPT distinguishes a hard prerequisite from “preferred before.” It also distinguishes a Gate, which asks whether a stated condition holds, from a Decision, which asks someone to choose. [`planning/SATISFIABILITY.md`][src-satisfiability] and [`planning/NODE_CONTRACTS.md`][src-nodes] develop those distinctions. The useful result for Foreman is simpler: some arrows leave him a choice, and some ask him to find evidence first.

<a id="smell-exploratory-dependencies"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Dependencies are planning judgments too. “M1 before M2” may be right for accepting a release and too strict for exploratory work. If the roadmap blocks the early phone experiment that could disprove the plan, we may have attached the dependency to the wrong thing.]]

<a id="guide-assignment"></a>

## Two good workers build two different versions of “resume”

The early phone experiment reveals no immediate obstacle. Foreman finishes the source-checking baseline and assigns two workers to the uploader: one handles the phone, the other the receiver.

He tells both to support resumable uploads.

The phone worker creates a new request ID for each retry. The receiver worker uses the request ID to identify the upload. Each implementation makes sense on its own. Together, they create a new upload whenever the phone reconnects.

Foreman could repair the integration himself. He does. But the incident also reveals that each worker received only a fragment of the same idea.

<a id="r-package"></a>

<!-- npt-rationale-definition: R-PACKAGE -->
Next time, he puts the common retry contract in writing and links each assignment to it. The assignment also names the source revision, the intended output, and who should receive the result.

NPT calls this a work package. Foreman uses [`templates/WORK_PACKAGE.md`][src-package] to prepare `planning/records/WP-17/rev1.md`. The record location is Harbor Sync's choice; the useful thing is the shared assignment, not that particular directory name.

Foreman writes the first prompt himself:

```text
Read WP-17/rev1, the linked retry contract, and its named source revision.
Implement the phone-side change. Choose the internal design.

Return a PR and a report of what you tested, what remains uncertain,
and whether any jobs are still running. Do not merge the PR.
Put the report at the result location in WP-17 and notify Foreman.
```

Here Foreman uses judgment to choose the task and its size. The package preserves the choice. The worker uses judgment to solve it. When the worker returns, Foreman checks the report against that same assignment rather than against his recollection of what he probably meant.

A reviewer can now ask, “Did they implement the agreed retry identity?” without reconstructing two conversations.

<a id="smell-package-repetition"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Today's work-package template contains much more than this little story needs. Some fields protect genuinely difficult recovery or delegation cases. Others may belong in inherited project configuration rather than every assignment. We should not use one useful handoff to justify unlimited repetition.]]

<a id="guide-roles"></a>

## Alex is still the wrong person to answer some questions

The workers find a harder problem: the receiver could retain incomplete uploads for days, or discard them quickly and ask the phone to restart. That affects cost, reliability, and the experience of someone with poor connectivity.

Foreman sends the question to Alex. Alex does not know enough about the design to settle it confidently, and he does not want Foreman to wait for every technical tradeoff.

He brings in Mara to lead the technical work.

<a id="r-roles"></a>

<!-- npt-rationale-definition: R-ROLES -->
They write a small division of responsibility. Mara may settle technical disputes and ordinary changes to the plan and working procedures within the agreed product promise and budget. Foreman continues to organize the work. Alex keeps the larger product and spending decisions. Mara also takes responsibility for deciding whether a result is ready to integrate or satisfies a milestone.

[`planning/ROLES.md`][src-roles] records those jobs and their current holders. It does not need to reproduce a corporate hierarchy. Mara might be a person or a useful long-lived agent context; either way, the team needs to know what question to bring to her.

Foreman reads that record, gives Mara the two options, and asks:

```text
Decide how long Harbor Sync should retain an incomplete upload.
Read the retry contract, the two implementation reports, and the cost estimate.
Explain your choice, its limits, and what the workers should change.
Return the decision at the supplied record location.
```

Mara chooses a bounded retention period. Foreman links her decision into the assignments and tells each worker what it changes. He does not rewrite her explanation into a different technical choice.

The Role matters when Mara later leaves. A replacement needs to know which responsibilities continue, not merely inherit a chat title.

<a id="smell-approval-ritual"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: “Ask Mara” could be genuine separation of responsibility or just another ritual. If she has no additional context, expertise, or accountability, why will her approval improve the choice? A second Role is not automatically a second useful judgment.]]

<a id="guide-morning"></a>

## Silence costs them a second implementation

One evening, a worker finishes its changes, but Foreman never receives the completion message. The next morning he starts another worker. Later, both return PRs.

Nobody misused authority. Foreman made a reasonable guess from incomplete information—and paid twice.

<a id="r-recovery"></a>

<!-- npt-rationale-definition: R-RECOVERY -->
For the next assignment, he keeps a record of the worker, the task, the expected return, and the next check. Harbor Sync calls that index `planning/EXECUTION_INVENTORY.md`, using NPT's [inventory template][src-inventory]. When a return goes missing, Foreman follows the recorded route before deciding to replace the worker.

This time he finds the completed report. Work resumes without another implementation.

If he cannot determine what happened, the inventory says so. An honest “unknown” gives tomorrow's Foreman a problem to investigate. An invented “never started” gives him a reason to repeat it.

<a id="r-records"></a>

<!-- npt-rationale-definition: R-RECORDS -->
Foreman also changes the order of his own work: he records the assignment before sending it. Otherwise, a crash between the send and the note would recreate the same uncertainty.

That small ordering choice explains part of the detail in `planning/EXECUTION.md`. Some records are not merely useful histories. They help the next actor avoid causing the same effect twice.

Foreman arranges a real follow-up with the available scheduler and records where it lives. He chooses a sensible interval; the scheduler supplies the wake. A promise in a chat does not do the scheduler's job.

<a id="smell-record-ordering"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Logging everything afterward and blocking everything until a log succeeds are both tempting simplifications. Neither fits every event. Which records protect an imminent effect, and which can wait for the learning system? Our architecture has to preserve that difference without making ordinary work depend on every optional archive.]]

<a id="guide-review"></a>

## Everyone who understands the implementation agrees with it

The uploader is ready for review. Foreman understands the design. Mara has discussed its hardest decisions. The implementer has tests for the behavior they intended.

They all look at the same code and see the same sensible approach.

Then Mara asks Foreman to commission someone who did not participate in those conversations. Foreman gives that reviewer the retry contract and exact source revision H41. The reviewer sends a deliberately awkward sequence of requests and finds that a retry can truncate a chunk the server already received.

The defect was not hidden in a mysterious algorithm. The familiar reviewers had all carried the same assumption into the review.

<a id="r-independence"></a>

<!-- npt-rationale-definition: R-INDEPENDENCE -->
Foreman does not need to forget the project. He needs to give this particular assignment to a context that did not help create the assumption. NPT's distinction between Role and holder helps here: calling an old collaborator “Cold Reviewer” does not change what that collaborator already knows.

Mara's familiarity remains useful for deciding what the finding means. The unfamiliar review and the informed decision do different jobs.

<a id="guide-review-prompt"></a>

### A useful prompt becomes a repeatable practice

After this experience, Mara asks Foreman to keep a review procedure for changes to upload state. Foreman drafts it; Mara agrees to use it. They call the revision **RV1**.

Harbor Sync keeps RV1 in `planning/LOCAL_PROCEDURES.md#review`. **That file is illustrative: it is not part of the linked NPT snapshot.** It is a convenient place for the project's own prompts and choices, not another universal layer the story requires us to invent.

RV1 asks for a fresh review of persistent-upload changes, allows Foreman to buy extra investigation within his budget, and brings repeated unresolved repair cycles back to Mara. Mara also includes changes to the review procedure itself: she wants someone to challenge them before they guide other work. These are local choices, not review counts that NPT imposes on every project.

Foreman keeps the prompt from the H41 review, separating its reusable wording from the exact source and result locations:

```text
Review the supplied base and head against the linked requirements.
Use your technical judgment. Look for concrete failures and missing cases;
do not invent objections merely to contribute.

Do not read earlier review conclusions or authoring conversations.
Return findings, source references, what you inspected, and the limits
of your checks at the supplied result location.
```

Foreman chose the reviewer and supplied the permitted inputs. The reviewer supplied the technical judgment. Foreman retains the report under `planning/records/RR-77/`; RV1 now gives future assignments a reusable starting point rather than a predetermined answer.

<a id="r-inputs"></a>

<!-- npt-rationale-definition: R-INPUTS -->
He also keeps the actual prompt. “Use RV1” would not reveal whether he added, “Mara thinks this implementation is fine.” The difference could explain the review better than the template name does.

<a id="smell-review-inputs"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Foreman can shape a review by selecting its inputs even when he never changes the prompt. Giving a reviewer everything would destroy some kinds of independence and waste attention. How do we preserve a fair question without pretending context selection contains no judgment?]]

<a id="guide-repair"></a>

## Repairing the bug does not answer every review question

Foreman sends the truncation finding to the original implementer, who returns revision `H42`. The reviewer had inspected `H41`; those names stand for exact source revisions, not moving branch names.

<a id="r-verification"></a>

<!-- npt-rationale-definition: R-VERIFICATION -->
Foreman now has two questions. Did the implementer fix the truncation? Did the repair leave or introduce another problem?

Mara asks Foreman to obtain both kinds of evidence for this repair. He returns to the original reviewer for the first and saves the reusable prompt in RV1's repair-verification section:

```text
Read the original truncation finding and the repair at H42.
Try the failure case and examine whether the change addresses it.
Return VERIFIED_RESOLVED, VERIFICATION_FAILED, or INCONCLUSIVE,
and explain what evidence supports that answer.
```

That verifier deliberately receives the earlier finding. For the second question, Foreman commissions a fresh review of H42 without the old conclusions. He preserves the two results separately. A new reviewer failing to rediscover a bug would not show that the repair fixed it.

The implementer can stay in the same productive conversation throughout. Freshness belongs to the assignment that needs it, not to a rule that every worker must disappear after every PR.

<a id="smell-review-stopping"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Review can become a machine for generating more review. A further pass may find a valuable defect, a debatable preference, or almost nothing. What outcome would persuade us to stop? We need to examine the cost of our local stopping rule, not treat another reviewer as automatically safer.]]

<a id="guide-integration"></a>

## “Ready” turns out to mean three different things

The implementer says H42 is ready. The reviewers report that they found no remaining concrete defect in their assigned scope. Mara still has to decide whether the project should merge it.

Those are different questions, even when everyone eventually answers yes.

<a id="r-integration"></a>

<!-- npt-rationale-definition: R-INTEGRATION -->
Foreman sends Mara a decision package using the short decision template they keep in `LOCAL_PROCEDURES.md#decision`:

```text
Decide whether to merge H42.
Read the candidate, its requirements, review and repair evidence,
and remaining limitations.
Return your decision and reasons for this exact candidate.
```

Mara approves H42. Foreman prepares to merge it using the local `#integration` procedure, which Mara agreed with him when she delegated the act of carrying out an approved merge.

This does not establish that every project needs Mara to approve every merge. She could delegate routine integration to Foreman and reserve exceptional cases. The important point is that the implementer's permission to prepare a change did not silently turn into permission to integrate anything it pleased.

<a id="r-current"></a>

<!-- npt-rationale-definition: R-CURRENT -->
Before merging, Foreman notices that the implementation branch now points to H43. The author made a cleanup edit after the review.

The edit may be harmless. Foreman still needs to deal with the change rather than pretend Mara approved it. He identifies what moved and brings H43 through the applicable review and decision steps. Mara confirms that revision; Foreman merges it and records the actual resulting state. An exact approval tells him what Mara decided; it does not follow a moving branch by magic.

The same lesson applies to instructions and authority. Foreman needs to know which version the project follows now, while retaining what governed earlier work. An unrelated change need not restart the world, but neither should a familiar-looking filename hide a material change.

The publication and execution documents supply that distinction in NPT. They are not an argument for asking Mara to approve typographical edits one at a time.

<a id="guide-field-evidence"></a>

### The phone still gets the last word

<a id="r-acceptance"></a>

<!-- npt-rationale-definition: R-ACCEPTANCE -->
After the merge, Foreman proposes marking the uploader milestone complete. Mara reads its criteria and the evidence, using [`templates/MILESTONE_ACCEPTANCE.md`][src-acceptance] as the record of her determination.

She accepts M2's software result. Foreman prepares the corresponding roadmap update through [`templates/PLAN_CHANGE.md`][src-change]. Mara approves the update, and Foreman publishes it. The shared plan now points to her acceptance and shows M2 as DONE. The receipt preserves what she judged; the roadmap tells later workers what the project currently counts as complete.

M3 remains open. The team still owes Alex a field trial. With M2 complete, Foreman arranges it—and the trial exposes a phone behavior the local fixtures did not reproduce. He routes the new failure back into work. The earlier test report remains an honest report of narrower evidence; nobody rewrites it to imply that it covered the field behavior.

<a id="r-evidence"></a>

<!-- npt-rationale-definition: R-EVIDENCE -->
This is why “tested,” “merged,” and “accepted” need something after them. Tested how? Merged which revision? Accepted against which promise?

A useful record need not be long. It needs to let the next reader distinguish an observation from a hope, and a missing measurement from a failed one.

<a id="smell-acceptance-handoffs"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Preserving those two facts does not necessarily require two separate human handoffs. Could one ordinary acceptance operation retain the judgment and update the shared view safely? We should not defend duplicated ceremony merely because the underlying facts are distinct.]]

<a id="smell-incomplete-assessments"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Final acceptances have an obvious home. Half-finished checks and inconclusive assessments can disappear into conversations. If we keep only the tidy endings, both maintainers and an EF will learn from a fictional version of the project's history.]]

<a id="guide-advice"></a>

## The review process starts to deserve its own review

Harbor Sync improves, but reviews now consume a noticeable part of the schedule. Some catch important failures; others repeat familiar observations. Foreman wants to know whether the team has found a good balance.

He consults two Experience Factories. EF-A recommends more independent review for persistent-state changes. EF-B recommends an additional pass only when the first leaves significant uncertainty.

<a id="r-advice"></a>

<!-- npt-rationale-definition: R-ADVICE -->
Foreman finds EF-A persuasive for one especially awkward PR and buys an extra review within RV1's allowance. He does not first need to turn the recommendation into a new local policy. He already has that choice.

But EF-B's recommendation cannot, by itself, remove a review RV1 requires. Foreman would then be changing the procedure rather than choosing within it.

Neither EF becomes Harbor Sync's manager. The team can compare both, inspect their evidence, or ignore their advice. A local habit of following one source automatically would deserve its own scrutiny; calling the source advisory would not explain who really controls the resulting choices.

<a id="smell-advice-rubber-stamp"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: We can preserve formal local approval while turning it into a rubber stamp for whichever EF sounds most confident. What evidence would show that local comparison adds value, rather than merely giving imported advice a local signature?]]

<a id="guide-planning-prompt"></a>

### Foreman asks for help, but does not outsource the question invisibly

Mara asks Foreman to investigate the review delays. This time he writes a planning assignment rather than sending a worker straight to edit RV1:

```text
Compare keeping RV1 with changing it.
Read the current plan, RV1, the named local review records, and the two
EF recommendations. Consider benefit, cost, uncertainty, and counterexamples.

Return NO_CHANGE with reasons, or a separate proposed edit and analysis.
State what you expect to improve and what should happen to reviews
already under way.
```

He records the actual inputs and sends the question to a planning worker. The worker writes `planning/records/PLN-9/report.md` and proposes **RV2**. Foreman keeps the full analysis, including counterarguments, while sending Mara a brief summary and links.

Here Foreman chose the question and the evidence scope. The worker judged the alternatives. Mara will decide whether to change the team's procedure. None of those judgments disappears behind “the system updated the policy.”

<a id="r-instructions"></a>

<!-- npt-rationale-definition: R-INSTRUCTIONS -->
The provenance of the instructions is now straightforward. Foreman drafted RV1 after the first missed retry defect; Mara adopted it. The planning worker drafted RV2 from the later comparison. If Mara adopts RV2, future Foremen can read what changed and what persuaded her.

They also keep the reusable part of this planning assignment as **PL1**, after Mara agrees to use it for future process investigations. Next time, Foreman can fill PL1's input slots rather than silently invent a different treatment. PL1 leaves the analysis to its worker; it does not promise that every worker will reach the same conclusion.

<a id="smell-procedure-packaging"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: The example's local procedure file is doing useful work that the current template does not package this way. Perhaps a few Markdown sections are enough. We should try them before deciding that each procedure needs its own schema, compiler, or repository.]]

<a id="guide-change"></a>

## A better rule does not get to approve itself

RV2 proposes fewer mandatory reviews for a narrow class of changes. Foreman still arranges the review of RV2 under RV1. Otherwise, the proposal could lower the bar while stepping over it.

<a id="r-adoption"></a>

<!-- npt-rationale-definition: R-ADOPTION -->
After that review, Foreman gives Mara the exact proposed text, the complete analysis, and the results. He uses the same decision template as before, but the question concerns the review procedure rather than a Product merge.

Mara can reject it, ask for another revision, or approve it. She approves RV2. That settles which procedure she wants the team to use. Foreman still has to work out the handoff from the old one.

Suppose the analyst instead proposes dropping source preservation to make the tests cheaper. Mara brings that to Alex. Their original arrangement left that product decision with him. The proposal can be sensible or foolish; its existence does not change who must consider it.

<a id="smell-amendment-path"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: “The old rules govern the change” must not become “the change may not differ from the old rules.” We need an intelligible amendment path, including a path for correcting goals. Otherwise the system preserves mistakes as carefully as commitments.]]

<a id="guide-active-work"></a>

## Mara agrees, but someone is halfway through the old instructions

Foreman prepares to announce RV2. Then he notices RR-78: a reviewer is still working under RV1. Another review is about to begin.

Should the first reviewer abandon a step already under way? Should both finish under the old procedure? A message saying "use RV2" leaves those questions to whoever happens to receive it.

Mara's decision was clear about the new procedure. It said too little about the people halfway through the old one.

<a id="r-active-work"></a>

<!-- npt-rationale-definition: R-ACTIVE-WORK -->
Foreman lists the affected work and brings the remaining question to Mara. She decides that RR-78 should finish under RV1 and new runs should use RV2. Foreman records that disposition with the change. He follows [`planning/PUBLICATION.md`][src-publication] and [`planning/PUBLICATION_TRANSITIONS.md`][src-transitions] to publish the agreed transition, then reconciles the inventory and tells the affected workers what applies to them.

If Mara instead calls for a pause, Foreman follows the request until he can establish what stopped. “I sent the message” and “the worker stopped its remaining jobs” answer different questions. [`templates/EXECUTION_RECEIPT.md`][src-receipt] helps preserve that distinction; [`templates/TRANSITION_ACTION.md`][src-transition-action] retains the agreed treatment of affected work.

There is a practical complication: someone could start another assignment while Foreman prepares the list. NPT specifies a publication/dispatch fence to prevent affected new work from slipping through that gap. The mechanism is detailed, but its reason is ordinary: the project should not change its instructions while losing track of who still uses the old ones.

The project also needs one discoverable answer to which change it actually adopted. A failed publication step cannot leave one worker following a new message while another follows the last complete publication. That is why NPT distinguishes an approval, a candidate commit, and the history that establishes current accepted state.

<a id="smell-publication-cost"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: This is where the simple story begins to require substantial infrastructure in today's NPT. Could a small, cooperative team get the same useful result with a simpler handoff? Which guarantees would that lose? We should answer those questions before presenting every field in the publication protocol as inevitable.]]

The story explains why shared currentness matters. It does not authorize a shortcut around the existing protocol. A lighter deployment would need its own explicit design; it should not arise because someone stopped reading a long document.

<a id="guide-continuity"></a>

## More work does not automatically mean more hierarchy

The field trial expands to several phones and locations. Foreman considers giving it a child plan.

At first he could simply keep several assignments under M3. That may still be best. A long list alone does not prove the need for another planning boundary.

<a id="r-nesting"></a>

<!-- npt-rationale-definition: R-NESTING -->
A child plan becomes attractive when a field lead can own the internal choices without making Mara follow every device and schedule. The parent would state what result it expects; the child would expose how its own contributors intend to deliver it.

Foreman uses PL1 to ask a planner to compare those arrangements. He includes [`planning/NESTING.md`][src-nesting], [`planning/REFERENCES.md`][src-references], and the exact M3 contract. The planner returns a proposed boundary, not a new authority structure already in force. Mara decides within her delegated scope; Foreman then uses the [child-plan][src-child-plan] and [child-role][src-child-roles] templates if the project adopts that arrangement.

Foreman can coordinate both plans. A useful field-lead chat can remain alive. Neither the number of chats nor the location of the files determines whether the project needs a child plan.

<a id="smell-nesting-or-storage"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Are we creating useful independence, or merely finding somewhere to put a large folder? Two teams can also pursue different plans for the same Product without one becoming the other's child. NPT should not manufacture hierarchy from storage layout or shared repository access.]]

<a id="guide-sharing"></a>

## The team contributes to learning without buying the answer

Alex sees value in the EF advice and sets aside a little worker capacity for process improvement. Foreman follows Harbor Sync's local sharing arrangement, offers fresh capacity to EF-A, and sends a separate request: investigating cold-review stopping rules would help them.

<a id="r-sharing"></a>

<!-- npt-rationale-definition: R-SHARING -->
EF-A's coordinator accepts the contribution. After consulting EF-A's own priorities, the coordinator assigns the worker to evidence cleanup instead. Alex did not restrict the gift to a particular task, so the recipient can make that choice.

Foreman has supplied resources and advice, not acquired control of EF-A. EF-A can return advice without acquiring control of Harbor Sync. The team's working plan and recovery records remain available locally even if EF-A disappears.

<a id="smell-donated-context"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A worker is not just a quantity of compute. Its conversation may contain private project context, and a shared account may expose more tools than the assignment needs. “Donate a worker” may need to mean fresh capacity with limited access, not handing over an already-informed chat.]]

<a id="guide-handoff"></a>

## Mara's memory is valuable—and finally unavailable

Mara's long-running context has become useful. She remembers why the first retry design failed and which field-test results remain suspicious. Foreman keeps it alive rather than repeatedly paying to rebuild it.

Then, one day, he cannot reach it.

The plan still names Mara's Role, but that does not tell a replacement why an apparently elegant design was rejected. The team has preserved its current commitments better than the thinking needed to question them.

<a id="r-context"></a>

<!-- npt-rationale-definition: R-CONTEXT -->
They begin leaving short handoff notes beside the actual work: accepted decisions and reasons, the most important failed approach, current revisions, open questions, and the next decision someone owes. They link the underlying reports rather than replace them with a polished summary.

The next lead does not inherit Mara's mind. The lead can now reconstruct enough to act, identify what remains uncertain, and decide where deeper reading will repay its cost.

Foreman needs the same protection. The inventory and procedure records should let a replacement recover outstanding work. A scheduler or operator must actually wake that replacement; a missing Foreman cannot promise to do it himself.

<a id="smell-handoff-reconstruction"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A handoff can look complete to its author and remain unusable to a newcomer. We may learn more by occasionally asking a fresh worker to find the next safe action than by requiring longer summaries. What would count as a successful reconstruction?]]

<a id="r-capabilities"></a>

<!-- npt-rationale-definition: R-CAPABILITIES -->
The experience also changes cleanup. Before Foreman retires a disposable context, he checks that its useful result survives and that no outstanding work still depends on it. He consults the capability records in the inventory rather than assume that archiving, deleting, and removing a containing project do the same thing.

He need not keep every chat forever. He needs to know what he will lose.

This distinction is especially important when one deletion would remove several people's work. A convenient cleanup action is not a reason to treat the surrounding project as disposable.

<a id="guide-purpose"></a>

## Could we still have said only “make Harbor Sync”?

Yes. That can remain Alex's opening request.

The difference is what Foreman leaves behind while fulfilling it. Instead of keeping all the project-defining decisions inside one conversation, he gives the team a shared promise, an exposed plan, understandable assignments, identifiable decisions, and enough history to continue after interruptions.

Alex may rarely need to intervene. The value of the shared plan is that he *can* intervene where it matters—and other contributors can work without asking him to reconstruct the project for them.

A capable Foreman might create all of those things on his own. In that case NPT is not making otherwise impossible work possible. It is offering a convention that other participants can recognize and reuse.

That is a more modest claim than “agents need NPT to do projects,” and a stronger foundation for the design.

<a id="smell-convention-or-engine"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Perhaps NPT's real product is an understandable collaboration convention, not an execution engine. If we explain its value mainly by showing Foreman running more machinery, we may be solving the wrong problem. Could another capable coordinator use the same public records without imitating Foreman's internals?]]

Nothing in this story proves that every team needs every record as a separate document, or every distinction as a separate actor. One small project might keep much of its shared understanding on a single page. A larger project may need stronger coordination and more precise handoffs.

The question for each addition is not “Does the ontology have a name for it?” It is “What went wrong without it, and does this repair help enough to keep?”

<a id="guide-links"></a>

## Why the rest of NPT should point back here

A year later, a maintainer reads an instruction telling Foreman to check an uncertain dispatch before retrying it. The maintainer wonders whether the check still matters.

<a id="r-traceability"></a>

<!-- npt-rationale-definition: R-TRACEABILITY -->
A nearby link to [R-RECOVERY](#r-recovery) brings them to the two implementations Foreman accidentally commissioned. Now they can evaluate the instruction rather than merely obey it. Perhaps the transport has gained reliable deduplication. Perhaps the check still protects an expensive effect. The story gives them a concrete reason to investigate.

That is the guide's canonical role: **the place we keep and challenge the reasons**, not a second copy of every operating procedure.

For example, a paragraph in `planning/EXECUTION.md` could carry:

```markdown
<!-- npt-rationale: R-RECOVERY R-RECORDS -->
Rationale: [Why Foreman checks before retrying](../guide.md#r-recovery)
and [why he records the assignment before sending](../guide.md#r-records).
```

The instructions own the exact procedure. The guide explains the problem the procedure addresses, the freedom it leaves, and the doubts that remain. A change to either should send maintainers back to the other.

Tags identify reasons, not frozen wording. When a reason no longer holds, we should revise it or leave a retirement note and simplify the instructions that depended on it. Historical records can still point to the older revision.

<a id="smell-rationale-quality"></a>

<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A link to a vague paragraph about “safety” could justify almost anything. A backlink checker can find a missing anchor; it cannot tell whether the linked argument deserves belief. Human review must still ask whether the example fits the restriction and whether a cheaper repair would work.]]

The guide should also make judgment visible. A maintainer should be able to say, “Here Foreman chooses the question; here he fills a prompt; here another worker analyzes it; here Mara decides.” That visibility does not require precomputing any of their answers.

If the guide only becomes readable when we hide an important handoff, that is a problem to revisit. If it only becomes complete after describing a huge new bureaucracy, that is another.

For the maintenance convention—stable anchors, specific backlinks, `cold-question` Issues, and the lifecycle of a Smell note—see [CONTRIBUTING.md](CONTRIBUTING.md). A skeptical question should improve this explanation or reveal something worth changing, not require a newcomer to recover our old conversations.

---

<a id="guide-sources"></a>

## Appendix: the documents the story earns

The main story introduces shared records as problems arise. **It does not describe a partially configured NPT deployment.** The linked [baseline][src-baseline] requires its current operational setup, including `transition-action-v1`, before Foreman-managed dispatch. A guide cannot introduce a lighter mode merely by telling a simpler story.

The repository links below follow the files in the revision you are reading. The guide foundation uses [NPT commit `d82b792`][src-baseline] as its source baseline; it does not claim an audit of every contract. When those files change, maintainers should revisit the associated explanation. An operational Foreman reads his project's applicable accepted versions, not this template repository's latest files.

| Need in the story | Where the inspected NPT stores the detail | What Foreman does with it |
|---|---|---|
| A shared promise and visible work ahead | [`planning/PLAN.md`][src-plan] | Reads outcomes, criteria, progress and dependencies; prepares proposed changes. |
| Understand his coordinating job | [`AGENTS.md`][src-agents]; [`prompts/FOREMAN.md`][src-foreman] | Reads the common obligations and uses the project's actual delegation to guide his choices. |
| Know which arrows leave a choice | [`planning/CONVENTIONS.md`][src-conventions]; [`planning/SATISFIABILITY.md`][src-satisfiability]; [`planning/NODE_CONTRACTS.md`][src-nodes] | Distinguishes prerequisites, preferences, Gates and Decisions; checks the relevant current evidence. |
| Find who can settle a question | [`planning/ROLES.md`][src-roles] | Resolves the Role, current holder and scope; routes the question and preserves the decision. |
| Give a worker an understandable assignment | [`templates/WORK_PACKAGE.md`][src-package]; [`planning/EXECUTION.md`][src-execution] | Records the task, exact inputs, permission, intended result and return route. |
| Recover a missing return or interrupted coordinator | [`templates/EXECUTION_INVENTORY.md`][src-inventory]; [`templates/EXECUTION_RECEIPT.md`][src-receipt] | Uses the configured inventory to discover work, results, actual follow-ups and unresolved requests. |
| Find what the project actually adopted | [`planning/PUBLICATION.md`][src-publication]; [`planning/PUBLICATION_TRANSITIONS.md`][src-transitions] | Resolves accepted history and follows the prescribed publication/recovery process. |
| Change the plan without forgetting active work | [`templates/PLAN_CHANGE.md`][src-change]; [`templates/TRANSITION_ACTION.md`][src-transition-action] | Prepares the change and its work impact for the appropriate decision; reconciles the published result. |
| Preserve what milestone acceptance meant | [`templates/MILESTONE_ACCEPTANCE.md`][src-acceptance] | Prepares evidence for the accepting holder; links the resulting receipt into the subsequent roadmap update. |
| Give a subteam useful independence | [`planning/NESTING.md`][src-nesting]; [`planning/REFERENCES.md`][src-references]; [`planning/PARENT.md`][src-parent]; [child templates][src-child-plan] | Checks the parent-facing promise and delegation; prepares or coordinates the adopted child boundary. |

`planning/EXECUTION_INVENTORY.md` is a configured project record, not an already-running inventory supplied by the template. Likewise, `planning/records/...` names illustrative Harbor Sync record locations. A real deployment chooses its durable stores and keeps runtime updates distinct from changes to its accepted planning documents.

<a id="guide-local-procedures"></a>

### Harbor Sync's illustrative local procedures

`planning/LOCAL_PROCEDURES.md` is not a delivered NPT file. It represents the short local procedures Foreman and Mara collect as the story progresses. Their actual content would need review and adoption in a real project.

| Section | Origin in the story | Use |
|---|---|---|
| `#coordination` | Alex grants ordinary discretion; Mara helps state the working boundaries. | Foreman chooses priorities and workers within that arrangement. |
| `#implementation` | Foreman saves the reusable part of the WP-17 prompt after the two incompatible implementations. | Foreman fills the task and references; the implementer returns a PR and report. |
| `#review` — RV1 | Foreman drafts the treatment after the missed truncation defect; Mara adopts it. | Foreman supplies the prompt and permitted inputs; a fresh reviewer supplies the technical judgment. |
| `#repair-verification` | Foreman and Mara add the distinct repair question to RV1. | Foreman supplies the finding and repair; the verifier returns a resolution result. |
| `#decision` | Foreman drafts the reusable decision request with Mara's agreement. | Foreman names the exact question and evidence; Mara decides within her Role. |
| `#integration` | Mara specifies how Foreman carries out an exact merge permission. | Foreman checks the candidate and applicable conditions, merges, and records the actual result. |
| `#planning` — PL1 | Foreman writes the review-delay investigation; Mara later adopts its reusable part. | Foreman fills the evidence scope; the planner returns analysis and a separate candidate, or no change. |
| `#sharing` | Alex approves a small contribution and its data limits. | Foreman offers capacity, evidence and a separate research request; the EF chooses its own response. |

The story's first assignments use prompts Foreman writes for those jobs. Later assignments can use accepted reusable templates. Keeping the actual prompt makes that transition visible; it does not force all future assignments into identical wording.

<a id="guide-rule-index"></a>

## Appendix: stable rationale tags

The 25 tags below identify reasons, not a checklist of new operational requirements. Their anchors sit beside the motivating passages; comments keep the identifiers out of the main reading path. Preserve their identities when reorganizing the guide.

**Existing** means the inspected template already expresses the core distinction. **Design** means the passage motivates a proposed direction, not a claim that the repository already implements it. The table points to likely backlink homes; it does not claim those backlinks exist yet.

| Tag | The question that earned it | Basis / likely backlink homes |
|---|---|---|
| [R-PROPORTION](#r-proportion) | Why not keep the arrangement that already works? | Design · guide and deployment choices |
| [R-SUCCESS](#r-success) | How can Foreman finish without silently choosing a different destination? | Existing outcome contracts; proposed broader rationale · `PLAN.md`, acceptance criteria |
| [R-VISIBILITY](#r-visibility) | How can other people question and contribute to work they cannot see? | Design emphasis supported by the roadmap · `PLAN.md`, Foreman prompt |
| [R-JUDGMENT](#r-judgment) | Why does Alex need a coordinator rather than another queue of questions? | Design · Foreman prompt, local delegation and procedures |
| [R-READINESS](#r-readiness) | Which ordering decisions belong to Foreman, and which need evidence? | Existing · conventions, satisfiability, node contracts |
| [R-PACKAGE](#r-package) | How do two workers know they are building the same thing? | Existing · work-package template and execution contract |
| [R-ROLES](#r-roles) | Who can answer the question without making Alex the bottleneck? | Existing · `ROLES.md`, `EXECUTION.md`, `AGENTS.md` |
| [R-RECOVERY](#r-recovery) | Why does silence not justify starting again? | Existing · execution, inventory, receipt records |
| [R-RECORDS](#r-records) | Why write some things down before the action? | Existing · dispatch, publication and inventory procedures |
| [R-INDEPENDENCE](#r-independence) | What can an unfamiliar reviewer see that collaborators miss? | Existing distinction · Roles and review requirements |
| [R-INPUTS](#r-inputs) | Which question did Foreman actually put to the worker? | Design · prompt and input records |
| [R-VERIFICATION](#r-verification) | Did we repair the old failure, or merely fail to notice it again? | Design · local review and repair procedures |
| [R-INTEGRATION](#r-integration) | What turns a reviewed candidate into a Product change? | Existing distinction · work grants and integration procedures |
| [R-CURRENT](#r-current) | Which exact change or instruction still applies now? | Existing · publication and execution contracts |
| [R-ACCEPTANCE](#r-acceptance) | What does a merged change establish about the promise? | Existing · acceptance and roadmap projection |
| [R-EVIDENCE](#r-evidence) | What did the test actually show? | Existing · return reports and criteria |
| [R-ADVICE](#r-advice) | When can useful advice change a choice without changing a rule? | Design · local procedures and EF interfaces |
| [R-INSTRUCTIONS](#r-instructions) | Who wrote this procedure, and why are we following it? | Design · procedure identity and adoption history |
| [R-ADOPTION](#r-adoption) | How can we change a rule without letting it approve itself? | Existing predecessor principle; broader design application · publication and plan changes |
| [R-ACTIVE-WORK](#r-active-work) | What about the people halfway through the old procedure? | Existing · execution, manifests and receipts |
| [R-NESTING](#r-nesting) | When does a child plan give someone useful independence? | Existing · nesting, references and child contracts |
| [R-SHARING](#r-sharing) | Why does funding an EF not buy its answer? | Design · resource and sharing arrangements |
| [R-CONTEXT](#r-context) | How can we keep a valuable mind without depending on its survival? | Design emphasis supported by recovery · handoff and inventory records |
| [R-CAPABILITIES](#r-capabilities) | What will this cleanup operation actually remove? | Existing · execution-context profiles and cleanup records |
| [R-TRACEABILITY](#r-traceability) | When can a maintainer safely remove an old instruction? | Design · specific rationale backlinks throughout the repository |

The inline **Smell** notes belong to the explanation, not to an operating checklist. They invite us to revisit a premise, a proposed repair, or its cost; they do not claim a verified defect or commission implementation. For this initial guide foundation, the 20 notes marked `untriaged-foundation` intentionally have no Issue links. After the foundation merges, a separate triage pass can link each concern to an existing or new Issue. We are preserving the questions here, not answering them by changing the rest of NPT.

The narrative and stable-anchor approach follow [Typed Planning's guide][src-tp-guide]. This guide does not adopt its ontology or require NPT to reproduce its classes.

<!-- Local links follow this repository revision; the baseline and TP inspiration remain pinned. -->

[src-baseline]: https://github.com/davrec72/nested-planning-template/tree/d82b792ba5ad565aba804e72578ff2c88f206caf
[src-agents]: AGENTS.md
[src-foreman]: prompts/FOREMAN.md
[src-plan]: planning/PLAN.md
[src-roles]: planning/ROLES.md
[src-conventions]: planning/CONVENTIONS.md
[src-satisfiability]: planning/SATISFIABILITY.md
[src-nodes]: planning/NODE_CONTRACTS.md
[src-nesting]: planning/NESTING.md
[src-references]: planning/REFERENCES.md
[src-parent]: planning/PARENT.md
[src-publication]: planning/PUBLICATION.md
[src-transitions]: planning/PUBLICATION_TRANSITIONS.md
[src-execution]: planning/EXECUTION.md
[src-package]: templates/WORK_PACKAGE.md
[src-inventory]: templates/EXECUTION_INVENTORY.md
[src-receipt]: templates/EXECUTION_RECEIPT.md
[src-change]: templates/PLAN_CHANGE.md
[src-transition-action]: templates/TRANSITION_ACTION.md
[src-acceptance]: templates/MILESTONE_ACCEPTANCE.md
[src-child-plan]: templates/CHILD_PLAN.md
[src-child-roles]: templates/CHILD_ROLES.md
[src-tp-guide]: https://github.com/davrec72/typed-planning/blob/bdfc63d3afbddefaad6c5f732c9e5b38295281b4/docs/guide.md
