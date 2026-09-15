# Why can't I just tell Foreman to do the whole project?

> “Foreman, make Harbor Sync for me. Tell me when it's done.”

If you came here from the README, that is the question this guide is meant to answer.

Alex does not want to manage an army of agents. In the smallest version of this story there are only three kinds of participants:

- **Alex**, who owns the project;
- **Foreman**, one persistent coordinator who is trusted to use judgment;
- **temporary workers**, created when implementation, research, or an independent review needs another context.

That may be the entire deployment. One person or one long-lived AI context can also hold several project Roles when the project does not need those judgments separated. NPT should not make a small project look like a bureaucracy merely because the vocabulary can describe a larger one.

*Harbor Sync, its people, prompts, and results are fictional. Repository links in the appendix point to the NPT baseline this guide foundation was drafted against.*

<a id="r-proportion"></a>
<!-- npt-rationale-definition: R-PROPORTION -->
The default should therefore be: **let Foreman run the project until a concrete failure earns another shared rule or record.**

<a id="smell-minimum-profile"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: If today's NPT cannot describe this small owner + Foreman + temporary-workers arrangement without dragging in infrastructure whose benefit has not yet appeared, perhaps the template's minimum profile is too heavy.]]

<a id="smell-story-bias"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A story can make almost any design look inevitable by arranging convenient failures. The problems below motivate distinctions; they do not prove that NPT's present machinery is the cheapest way to preserve them. A simpler repair is a reason to change the design, not a failure to appreciate it.]]

## The whole argument on one page

Before Harbor Sync gets complicated, here is the progression this guide will try to justify.

| Start with | What goes wrong | Smallest repair the story earns |
|---|---|---|
| “Foreman, build it.” | Foreman makes a reasonable tradeoff Alex never wanted. | Make the **desired outcome** visible. |
| Foreman keeps the route in his head. | Alex cannot question priorities until after the work is sunk. | Expose the **plan**. |
| Workers get conversational assignments. | Two good workers implement incompatible interpretations. | Preserve an understandable **assignment**. |
| Completion arrives through chat. | Silence looks like failure; Foreman duplicates work. | Keep **durable execution state**. |
| Familiar collaborators review their own assumptions. | Everyone misses the same defect. | Use **independent review when it buys something**. |
| “Ready” is one vague state. | Implementation, review, merge, and milestone success blur together. | Name the **decision being made** and preserve its evidence. |
| A procedure changes informally. | New work and old work quietly follow different rules. | Make the **current rule and its change** visible. |

That is the compression layer. Everything else in this guide should either explain one of those repairs, show where Foreman still uses judgment, or expose a place where NPT may have gone further than the failure really requires.

## What a small project should feel like

A normal day need not involve all of NPT's machinery.

```text
Alex and Foreman share the outcome and visible plan.
        ↓
Foreman chooses useful work and commissions a worker.
        ↓
The worker returns a concrete result and evidence.
        ↓
Foreman gets whatever review or decision the current plan actually requires.
        ↓
The accepted result becomes part of the shared project state.
        ↓
Foreman chooses the next useful work.
```

Foreman does the coordinating. Alex does not approve every scheduling choice. Temporary workers need not become permanent Roles. A review is not required merely because another context exists.

The rest of the guide asks why even this modest arrangement needs any durable structure at all.

---

<a id="guide-job"></a>
<a id="guide-example"></a>
## Foreman delivers the wrong Harbor Sync

Foreman gets to work. He builds an uploader, a progress display, and automatic retries. To save space, he compresses videos before upload. To simplify the server, he gives each uploaded file a new timestamp.

A few days later, Alex opens the app. It works. Then he downloads a recording.

“This isn't the original file.”

Foreman explains the tradeoff. Smaller files upload faster, and the server's timestamps make sorting convenient.

“But these are my source recordings,” Alex says. “Preserving them is the point.”

Foreman has not betrayed Alex. He has filled in a decision Alex never expressed. More intelligence might have prompted him to ask earlier, but it could not have made an unstated preference certain.

They could try a stronger instruction: “Build exactly what I mean.” That would leave the same problem underneath.

Instead, they write down the promise:

> Harbor Sync uploads recordings without changing their bytes or original recording timestamps. Interrupted uploads can resume. The first release must work on an actual phone with an unreliable connection, not just in a desktop demonstration.

Alex changes one phrase. Now both of them can point to the same destination.

<a id="r-success"></a>
<!-- npt-rationale-definition: R-SUCCESS -->
The useful restriction is small. Alex has not chosen Foreman's architecture. He has made the **success condition public**.

Foreman may still choose the interface, protocol, tools, and implementation. He may argue that the promise should change. What he should not do is silently replace it with a more convenient promise and later call that success.

NPT gives these shared outcomes and acceptance criteria a home in [`planning/PLAN.md`][src-plan].

<a id="smell-changing-goals"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Alex may discover another important preference only after using the app. A written goal does not finish the conversation or make his first wording infallible. Does NPT make it easy to refine an honest misunderstanding, or does it encourage everyone to defend an obsolete contract because it is already “accepted”?]]

<a id="guide-visible-plan"></a>
## “What are you going to do next?”

Foreman removes the compression and fixes timestamp handling. Alex asks when he can try Harbor Sync on his phone.

Foreman says Friday.

On Friday, the server is fast, but nobody has tried a disconnected phone. Foreman spent the week improving throughput. He thought the field trial would be more useful afterward.

Alex would have preferred a rough field trial on Tuesday. A failure there could have changed the whole design.

Foreman did not make an irrational choice. The problem is that the route existed only inside the coordinator who was choosing it.

So Foreman exposes a short plan:

| Outcome | Evidence that would matter | Dependency for acceptance |
|---|---|---|
| M1: unchanged recordings arrive | Compare source and received bytes and recording metadata | none |
| M2: uploads survive interruption | Run the agreed interruption cases | M1 |
| M3: first release works in the field | Trial on an actual phone | M2 for release acceptance |

Foreman also proposes an early phone experiment. It cannot establish M3 yet, but it can challenge the plan cheaply. Alex agrees.

<a id="r-visibility"></a>
<!-- npt-rationale-definition: R-VISIBILITY -->
**An exposed plan makes delegation discussable before the consequences are sunk.**

Alex can question priorities without becoming the scheduler. A worker can see why an assignment matters. A reviewer can see what the project means to establish. A successor Foreman can see what remains open.

The plan is not a transcript of Foreman's private reasoning. It is the shared account of the commitments the project is currently following. NPT uses `planning/PLAN.md` for that roadmap and [`planning/CONVENTIONS.md`][src-conventions] for the small vocabulary used to read it.

<a id="smell-unused-roadmap"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A polished roadmap can become another report that nobody works from. If Foreman maintains one plan in his head and a reassuring one in `PLAN.md`, we have added work without adding visibility. The guide should help us ask whether the shared plan actually influences assignments and decisions.]]

## The plan should not take Foreman's job away

Alex is pleased with the visibility—until Foreman starts asking whether to investigate a failed retry before improving the progress display, whether to create a second worker, and whether to keep yesterday's useful implementation context alive.

“I wanted to see the plan,” Alex says. “I didn't ask to become the scheduler.”

They have overcorrected.

<a id="r-judgment"></a>
<!-- npt-rationale-definition: R-JUDGMENT -->
Alex tells Foreman to make ordinary coordination choices himself. Foreman has a working budget and room to choose priorities, workers, and extra investigation. Alex still wants the choices that would change Harbor Sync's purpose, exceed an agreed resource boundary, or settle a decision he deliberately kept.

Foreman investigates the retry failure first. Another good Foreman might investigate it in parallel with interface work. NPT does not need to decide which is wiser in advance.

The reason for the shared plan is to expose the important commitments, not to turn Foreman into a deterministic workflow engine. [`prompts/FOREMAN.md`][src-foreman] describes the coordination job; the project's accepted authority says how much discretion its holder has.

<a id="r-readiness"></a>
<!-- npt-rationale-definition: R-READINESS -->
Some ordering choices are nevertheless different from preferences. Foreman may move interface work around. He should not claim M2 is established before the project has the evidence M2 depends on.

That is the reason NPT distinguishes a hard prerequisite from a mere “preferred before,” and an objective Gate from a Decision that needs judgment. [`planning/SATISFIABILITY.md`][src-satisfiability] and [`planning/NODE_CONTRACTS.md`][src-nodes] hold the detailed contracts. The human point is simpler: **some arrows leave Foreman room to choose; some say what must be true before a later claim is honest.**

<a id="smell-exploratory-dependencies"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Dependencies are planning judgments too. “M1 before M2” may be right for accepting a release and too strict for exploratory work. If the roadmap blocks the early phone experiment that could disprove the plan, we may have attached the dependency to the wrong thing.]]

<a id="guide-assignment"></a>
## Two good workers build two different versions of “resume”

The early phone experiment reveals no immediate obstacle. Foreman assigns one worker to the phone and another to the receiver.

He tells both to support resumable uploads.

The phone worker creates a new request ID for each retry. The receiver treats the request ID as the upload identity. Each implementation makes sense alone. Together, they create a new upload whenever the phone reconnects.

Foreman can repair the integration. The incident still reveals that two workers received only fragments of the same idea.

<a id="r-package"></a>
<!-- npt-rationale-definition: R-PACKAGE -->
Next time, Foreman preserves the common retry contract and links each assignment to it. The assignment also names the exact source revision, the intended result, and where the worker should return it.

NPT calls this a **work package**. The template lives at [`templates/WORK_PACKAGE.md`][src-package].

A small package can yield a small prompt:

```text
Read this assignment, the linked retry contract, and the named source revision.
Implement the phone-side change. Choose the internal design.

Return a PR plus what you tested, what remains uncertain,
and whether any jobs are still running. Do not merge the PR.
Return the result to Foreman at the location named in the assignment.
```

Foreman chose the task and its size. The package preserves that choice. The worker still chooses how to solve it.

The value is not paperwork for its own sake. Later, a reviewer can ask “did this implement the shared retry identity?” without reconstructing two conversations.

<a id="smell-package-repetition"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Today's work-package template contains much more than this little story needs. Some fields protect genuinely difficult recovery or delegation cases. Others may belong in inherited project configuration rather than every assignment. We should not use one useful handoff to justify unlimited repetition.]]

## Do we need another permanent lead?

The workers find a harder design question: the receiver could retain incomplete uploads for days, or discard them quickly and ask the phone to restart. Alex does not want to become the technical bottleneck.

For Harbor Sync he introduces Mara, who knows the technical context and can settle ordinary technical disputes.

A smaller project could skip Mara. Alex could keep those decisions. Foreman could hold the relevant substantive Role too if Alex deliberately delegated it. **Role names are not a requirement for separate chats.**

<a id="r-roles"></a>
<!-- npt-rationale-definition: R-ROLES -->
The useful fact is the responsibility that survives holder changes: which questions may Mara settle, which remain Alex's, and which are Foreman's coordination choices?

[`planning/ROLES.md`][src-roles] records those responsibilities and their current holders. It should not reproduce an imaginary corporate hierarchy.

Foreman gives Mara the options and the relevant evidence. Mara decides on a bounded retention period. Foreman routes that decision back into the work.

<a id="smell-approval-ritual"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: “Ask Mara” could be genuine separation of responsibility or just another ritual. If she has no additional context, expertise, or accountability, why will her approval improve the choice? A second Role is not automatically a second useful judgment.]]

<a id="guide-morning"></a>
## Silence costs them a second implementation

One evening, a worker finishes, but Foreman never receives the completion message. The next morning he assumes the work did not happen and starts another worker. Later, both return PRs.

Nobody acted maliciously. Foreman made a reasonable guess from incomplete information—and paid twice.

<a id="r-recovery"></a>
<!-- npt-rationale-definition: R-RECOVERY -->
For the next assignment, Foreman keeps a durable record of the worker, the exact task, the expected return, and the next check. Harbor Sync uses the execution inventory described by [`planning/EXECUTION.md`][src-execution] and [its template][src-inventory].

When a return goes missing, Foreman reconciles the recorded attempt before replacing it.

If he still cannot determine what happened, the durable answer is **unknown**. “Unknown” gives the next Foreman something to investigate. “Never started” invents permission to repeat the effect.

<a id="r-records"></a>
<!-- npt-rationale-definition: R-RECORDS -->
Foreman also records a material assignment before sending it. Otherwise a crash between the send and the note recreates the same uncertainty.

That explains why some execution records are more than retrospective logs. They make recovery possible.

Foreman schedules a real follow-up when the substrate supports one and records where it lives. A sentence saying “I'll check later” does not create a wakeup.

<a id="smell-record-ordering"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Logging everything afterward and blocking everything until a log succeeds are both tempting simplifications. Neither fits every event. Which records protect an imminent effect, and which can wait for the learning system? Our architecture has to preserve that difference without making ordinary work depend on every optional archive.]]

<a id="guide-review"></a>
## Everyone who understands the implementation agrees with it

The uploader reaches review. Foreman understands the design. Mara discussed the difficult choices. The implementer tested the behavior they intended.

They all see the same sensible approach.

Then Mara asks Foreman for a reviewer who did not participate in those conversations. The fresh reviewer tries an awkward retry sequence and finds that a retry can truncate a chunk the server already received.

The defect was not obscure. The familiar participants carried the same assumption into the review.

<a id="r-independence"></a>
<!-- npt-rationale-definition: R-INDEPENDENCE -->
The lesson is not “always add another reviewer.” It is that **independence belongs to the context that needs it**. Renaming an authoring chat “Reviewer” does not erase what it already knows.

The informed participants remain useful for deciding what the finding means. The cold reviewer contributes a different kind of evidence.

Foreman can keep the review prompt short:

```text
Review the supplied base and head against the linked requirements.
Use your technical judgment. Look for concrete failures and missing cases.
Do not read earlier review conclusions or authoring conversations.
Return findings, what you inspected, and the limits of your checks.
```

<a id="r-inputs"></a>
<!-- npt-rationale-definition: R-INPUTS -->
Keeping the actual prompt and input set matters because “use the review procedure” does not reveal whether Foreman also said, “Mara thinks this implementation is fine.”

<a id="smell-review-inputs"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Foreman can shape a review by selecting its inputs even when he never changes the prompt. Giving a reviewer everything would destroy some kinds of independence and waste attention. How do we preserve a fair question without pretending context selection contains no judgment?]]

## Fixing the old bug is not the same question as reviewing the new code

The implementer returns a repair.

<a id="r-verification"></a>
<!-- npt-rationale-definition: R-VERIFICATION -->
Foreman now has two useful questions:

1. Did this repair actually fix the specific truncation failure?
2. What problems remain in the repaired candidate?

For the first, the verifier should know the original finding. For the second, a fresh reviewer should not be primed by all of the earlier conclusions.

Those treatments can use the same people or models when independence does not matter, but they should not be confused merely because both are called “review.”

<a id="smell-review-stopping"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Review can become a machine for generating more review. A further pass may find a valuable defect, a debatable preference, or almost nothing. What outcome would persuade us to stop? We need to examine the cost of our local stopping rule, not treat another reviewer as automatically safer.]]

<a id="guide-integration"></a>
## “Ready” turns out to mean several things

The implementer says the repair is ready. The reviewers report no remaining concrete defect in their assigned scope. Someone still has to decide whether this exact candidate should become the Product state.

<a id="r-integration"></a>
<!-- npt-rationale-definition: R-INTEGRATION -->
Those facts should not become one vague “ready” bit. The implementer can be allowed to prepare a change without being allowed to merge anything it pleases. A clean review can be useful evidence without becoming merge authority.

For Harbor Sync, Mara keeps the integration decision. Another project may delegate ordinary merges to Foreman and reserve only exceptional cases. The separation is about **which decision was delegated**, not about requiring another human ceremony.

<a id="r-current"></a>
<!-- npt-rationale-definition: R-CURRENT -->
Before the merge, Foreman notices that the branch now contains another cleanup commit. It may be harmless, but it is not the exact candidate the reviewer and Mara considered.

Foreman deals with the actual revision rather than pretending the earlier decision followed a moving branch automatically.

The same principle later matters for plans, instructions, and authority: historical records tell us what governed earlier work; the project also needs a discoverable answer to what governs the next action.

### The phone still gets the last word

<a id="r-acceptance"></a>
<!-- npt-rationale-definition: R-ACCEPTANCE -->
After integration, Foreman asks whether the milestone's promised outcome is actually satisfied. That is a different question from “did the code merge?”

Mara compares the evidence against the milestone criteria and records her determination using [`templates/MILESTONE_ACCEPTANCE.md`][src-acceptance]. The shared roadmap then reflects what the project currently counts as complete.

M3 remains open until the field trial. When the phone exposes a behavior the fixtures missed, Foreman routes that failure back into work rather than rewriting the narrower test as if it had proved more than it did.

<a id="r-evidence"></a>
<!-- npt-rationale-definition: R-EVIDENCE -->
This is why “tested,” “merged,” and “accepted” need an object after them: tested **what**, against **which revision**, and accepted against **which promise**?

A useful record need not be long. It needs to keep observation, decision, and missing evidence from collapsing into one tidy success story.

<a id="smell-acceptance-handoff"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Preserving those two facts does not necessarily require two separate human handoffs. Could one ordinary acceptance operation retain the judgment and update the shared view safely? We should not defend duplicated ceremony merely because the underlying facts are distinct.]]

<a id="smell-incomplete-evidence"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Final acceptances have an obvious home. Half-finished checks and inconclusive assessments can disappear into conversations. If we keep only the tidy endings, both maintainers and later process analysis will learn from a fictional version of the project's history.]]

## At this point, stop adding machinery unless another problem appears

The small project already has the core things that earned their keep in the story:

```text
visible outcome
visible plan
Foreman judgment inside delegated bounds
understandable assignments
durable execution state
review when independence matters
explicit decisions and evidence
```

That is enough to run a lot of work.

The next sections describe complications that **some** long-running projects encounter. They are not evidence that every NPT deployment should expose every publication field, child-plan contract, or external-learning interface to every maintainer.

<a id="smell-product-boundary"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Perhaps NPT's real product is an understandable collaboration convention, not an execution engine. If we explain its value mainly by showing Foreman running more machinery, we may be solving the wrong problem. Could another capable coordinator use the same public records without imitating Foreman's internals?]]

---

## Complication: the project's own procedure changes

Harbor Sync has now repeated the review pattern enough times to write down a reusable local review procedure. Later, someone proposes a better one.

<a id="r-instructions"></a>
<!-- npt-rationale-definition: R-INSTRUCTIONS -->
Once a procedure actually governs work, maintainers need to know **which version was in force and why the project follows it**. A prompt name without its content and provenance is too easy to reinterpret later.

The current procedure can still leave judgment to Foreman and reviewers. Reusability does not imply deterministic answers.

<a id="smell-local-procedure"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A few Markdown sections may be enough to preserve useful local procedures. We should try the smallest representation before deciding that each procedure needs its own schema, compiler, or repository.]]

<a id="guide-change"></a>
### A better rule does not get to approve itself

Suppose the proposal lowers the mandatory review required for persistent-state changes.

<a id="r-adoption"></a>
<!-- npt-rationale-definition: R-ADOPTION -->
The proposed weaker rule should not become the rule used to decide whether the proposal itself received enough review. The incumbent procedure governs the transition that replaces it.

That is the concrete reason behind NPT's broader predecessor principle: a candidate may propose new rules, but it does not receive power from those rules before they are adopted.

<a id="smell-amendment-path"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: “The old rules govern the change” must not become “the change may not differ from the old rules.” We need an intelligible amendment path, including a path for correcting goals. Otherwise the system preserves mistakes as carefully as commitments.]]

## Complication: someone is halfway through the old procedure

Mara approves the new review procedure. One review is already underway under the old one; another has not started.

Should both restart? Should the first finish where it began? The new text alone does not answer that question.

<a id="r-active-work"></a>
<!-- npt-rationale-definition: R-ACTIVE-WORK -->
For Harbor Sync, Mara decides that the existing review finishes under the old procedure and new reviews use the new one. Foreman records that disposition and tells the affected workers.

The reason is modest: **changing a shared rule should not make existing work ambiguous.**

Today's NPT implements strong currentness and recovery guarantees through its publication and execution contracts. The details are substantial. They live in [`planning/PUBLICATION.md`][src-publication], [`planning/PUBLICATION_TRANSITIONS.md`][src-transitions], [`planning/EXECUTION.md`][src-execution], and the transition templates rather than in this introductory story.

<a id="smell-publication-complexity"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: This is where a simple human requirement—“know which rule is current and do not lose active work while changing it”—turns into substantial machinery in today's NPT. Could a small, cooperative deployment preserve the useful guarantee with less infrastructure? Which failure modes would it knowingly give up?]]

<a id="smell-projection-necessity"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: NPT currently separates an authoritative milestone acceptance from the later roadmap state that makes the acceptance operationally visible to downstream work. The facts are genuinely distinct; it is still fair to ask whether every deployment needs a separate projection transition rather than one atomic accepted operation that preserves both facts.]]

## Complication: one outcome becomes a project of its own

The field trial expands to many devices, locations, and schedules. Foreman could keep all of those assignments under M3. At some point that stops helping the people doing the field work.

<a id="r-nesting"></a>
<!-- npt-rationale-definition: R-NESTING -->
A child plan earns its existence when another coordinator or team needs a **visible local plan and real freedom over its internal route**, while the parent keeps the outcome and boundary it cares about.

The parent can say “demonstrate reliable field operation under these criteria.” The child can decide how to schedule devices, divide work, and investigate failures inside that boundary.

[`planning/NESTING.md`][src-nesting] and [`planning/REFERENCES.md`][src-references] describe that relationship. A large folder does not itself justify a child plan, and the same Foreman may coordinate both if that remains useful.

<a id="smell-nesting-boundary"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Are we creating useful independence, or merely finding somewhere to put a large folder? Two teams can also pursue different plans for the same Product without one becoming the other's child. NPT should not manufacture hierarchy from storage layout or shared repository access.]]

<a id="smell-nested-name"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: Nesting is powerful but optional in this story. If the project is named “nested-planning-template” while most of its everyday value comes from visible plans, delegation, recovery, and review, does the name overstate one mechanism and hide the broader purpose?]]

## Complication: advice comes from outside the project

An **Experience Factory (EF)** is an external process that studies evidence from past work and publishes recommendations about how work might be done better. It has no authority over Harbor Sync merely because its analysis is persuasive.

<a id="guide-advice"></a>
<a id="r-advice"></a>
<!-- npt-rationale-definition: R-ADVICE -->
If an EF recommends an extra review and Foreman already has discretion to buy one, he can use the recommendation just like any other evidence. He does not need to adopt a new policy first.

If the EF recommends removing a review the current local procedure requires, that is a proposal to change the procedure. The distinction is between **advice inside existing discretion** and **changing the rule that defines the discretion**.

<a id="smell-ef-rubber-stamp"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: We can preserve formal local approval while turning it into a rubber stamp for whichever EF sounds most confident. What evidence would show that local comparison adds value, rather than merely giving imported advice a local signature?]]

<a id="r-sharing"></a>
<!-- npt-rationale-definition: R-SHARING -->
Harbor Sync may also contribute evidence or worker capacity back to an EF. Funding does not make the donor the EF's manager; receiving a recommendation does not make the EF Harbor Sync's manager.

That interface matters to the larger ecosystem, but a project can use NPT without any EF at all.

<a id="smell-worker-context-sharing"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A worker is not just a quantity of compute. Its conversation may contain private project context, and a shared account may expose more tools than the assignment needs. “Donate a worker” may need to mean fresh capacity with limited access, not handing over an already-informed chat.]]

## Complication: the useful long-lived context disappears

Mara has accumulated months of valuable context. Keeping that context alive is rational. Then it becomes unavailable.

<a id="guide-handoff"></a>
<a id="r-context"></a>
<!-- npt-rationale-definition: R-CONTEXT -->
The goal is not to pretend a replacement can recreate Mara's mind. The goal is that the project does not lose the decisions, open questions, current revisions, and next obligations that made her context operationally indispensable.

Long-lived contexts are useful caches. They should not be the only copies of project-defining state.

<a id="smell-handoff-quality"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A handoff can look complete to its author and remain unusable to a newcomer. We may learn more by occasionally asking a fresh worker to find the next safe action than by requiring longer summaries. What would count as a successful reconstruction?]]

<a id="r-capabilities"></a>
<!-- npt-rationale-definition: R-CAPABILITIES -->
The same caution applies when Foreman cleans up old contexts and schedules. “Archive,” “delete,” and “remove the container” may have different consequences on the actual platform. NPT therefore records capabilities where cleanup and recovery depend on them rather than inferring universal behavior from one remembered experiment.

Again, the reason is recovery, not a desire to model every platform feature.

---

## Could we still have said only “make Harbor Sync”?

Yes. That can remain Alex's opening request.

The difference is what Foreman leaves visible while fulfilling it:

```text
a shared promise
an exposed plan
understandable assignments
recoverable work state
identifiable decisions
evidence that says what it actually established
```

Alex may rarely intervene. Other contributors can still see what they are contributing to. A replacement coordinator can resume without treating missing conversation history as a blank slate.

A capable Foreman might invent all of those practices on his own. In that case NPT is not making otherwise impossible work possible. It is giving participants a convention they can recognize, inspect, challenge, and reuse.

That is deliberately a modest claim.

Nothing in this guide proves that every record deserves its own document, that every distinction needs a separate Role, or that every project needs the strongest recovery protocol. The maintenance question is always:

> **What concrete failure does this rule prevent, and is this still the cheapest understandable repair?**

<a id="guide-links"></a>
## Why the rest of NPT should point back here

A year later, a maintainer reads an instruction telling Foreman to reconcile an uncertain dispatch before retrying it. The maintainer wonders whether the check still matters.

<a id="r-traceability"></a>
<!-- npt-rationale-definition: R-TRACEABILITY -->
A nearby link to [R-RECOVERY](#r-recovery) brings them to the duplicate implementation caused by silence. Now they can evaluate the instruction rather than merely preserve it.

Perhaps the transport has gained reliable deduplication. Perhaps the check still protects an expensive effect. The rationale gives the maintainer a concrete question.

That is what this guide should make canonical: **the reasons we keep and challenge**, not a second copy of every operating procedure.

An operational document can point back with a specific tag:

```markdown
<!-- npt-rationale: R-RECOVERY R-RECORDS -->
Rationale: [why silence does not justify redispatch](../guide.md#r-recovery)
and [why the assignment is recorded before send](../guide.md#r-records).
```

The operational document owns the exact procedure. The guide owns the reason for the procedure and the doubts that remain.

<a id="smell-rationale-link-quality"></a>
<!-- npt-smell-status: untriaged-foundation -->
[[**Smell**: A link to a vague paragraph about “safety” could justify almost anything. A backlink checker can find a missing anchor; it cannot tell whether the linked argument deserves belief. Human review must still ask whether the example fits the restriction and whether a cheaper repair would work.]]

The guide should also keep judgment visible. A maintainer should be able to say, “Here Foreman chose the next task; here another worker supplied technical analysis; here a holder exercised a reserved decision.” We do not need to record private chain-of-thought to preserve those public responsibilities.

If the explanation of a rule repeatedly requires unrelated machinery, that is not automatically a documentation problem. It may be the guide telling us to simplify NPT.

---

<a id="guide-sources"></a>
## Appendix: where the story maps into the repository

This appendix is a map, not a reading order. A cold reader does **not** need to understand all of these documents before understanding the guide.

The links pin the NPT baseline on which this guide foundation was drafted. An operational Foreman reads the applicable accepted versions for its own project.

### The small-project core

| Need earned in the story | Primary NPT home |
|---|---|
| Visible outcome, roadmap, and milestone criteria | [`planning/PLAN.md`][src-plan] |
| Roadmap vocabulary and dependency meaning | [`planning/CONVENTIONS.md`][src-conventions] |
| Responsibilities and current holders | [`planning/ROLES.md`][src-roles] |
| Foreman's coordinating job | [`prompts/FOREMAN.md`][src-foreman] |
| Bounded worker assignments and execution/recovery rules | [`templates/WORK_PACKAGE.md`][src-package], [`planning/EXECUTION.md`][src-execution] |
| Durable coordination state | [`templates/EXECUTION_INVENTORY.md`][src-inventory] |
| Milestone acceptance | [`templates/MILESTONE_ACCEPTANCE.md`][src-acceptance] |

### Machinery that appears only when the corresponding complication appears

| Complication | Primary NPT home |
|---|---|
| Exact current planning state and changing accepted instructions while work exists | [`planning/PUBLICATION.md`][src-publication], [`planning/PUBLICATION_TRANSITIONS.md`][src-transitions], [`templates/PLAN_CHANGE.md`][src-change], [`templates/TRANSITION_ACTION.md`][src-transition-action] |
| Decision/DATA activation and readiness details | [`planning/SATISFIABILITY.md`][src-satisfiability], [`planning/NODE_CONTRACTS.md`][src-nodes] |
| Child plans and cross-plan references | [`planning/NESTING.md`][src-nesting], [`planning/REFERENCES.md`][src-references], [`planning/PARENT.md`][src-parent] |
| Material request receipts and uncertain stop/application state | [`templates/EXECUTION_RECEIPT.md`][src-receipt] |

`AGENTS.md` summarizes repository-wide invariants, but this guide deliberately does not use it as an introductory dump. The point of the guide is to explain why those invariants exist before asking maintainers to preserve them.

<a id="guide-rule-index"></a>
## Appendix: stable rationale tags

The tags below are durable documentation identifiers. **Existing** means the inspected template already expresses the core distinction. **Design** means the passage motivates a direction or maintenance principle rather than claiming the repository already implements that exact representation.

| Tag | The question that earned it | Basis / likely backlink homes |
|---|---|---|
| [R-PROPORTION](#r-proportion) | Why not keep the arrangement that already works? | Design · guide and deployment choices |
| [R-SUCCESS](#r-success) | How can Foreman finish without silently choosing a different destination? | Existing · plan outcome and acceptance criteria |
| [R-VISIBILITY](#r-visibility) | How can other participants question work before it is sunk? | Existing roadmap; guide emphasis |
| [R-JUDGMENT](#r-judgment) | Why does Alex need a coordinator rather than another queue of approvals? | Design · Foreman prompt and local delegation |
| [R-READINESS](#r-readiness) | Which ordering choices belong to Foreman, and which claims need evidence first? | Existing · conventions, satisfiability, node contracts |
| [R-PACKAGE](#r-package) | How do workers know they are building the same thing? | Existing · work package and execution contract |
| [R-ROLES](#r-roles) | Who is responsible for which reserved judgment? | Existing · roles and execution authority |
| [R-RECOVERY](#r-recovery) | Why does silence not justify starting again? | Existing · execution and inventory contracts |
| [R-RECORDS](#r-records) | Why write some facts before the effect? | Existing · execution/publication recovery rules |
| [R-INDEPENDENCE](#r-independence) | What can an unfamiliar reviewer see that collaborators miss? | Existing distinction; review requirements |
| [R-INPUTS](#r-inputs) | Which question and context did Foreman actually give the reviewer? | Design · prompt/input provenance |
| [R-VERIFICATION](#r-verification) | Did we repair the old failure, or merely fail to rediscover it? | Design · review/repair procedure |
| [R-INTEGRATION](#r-integration) | What turns a prepared/reviewed candidate into Product state? | Existing authority distinction |
| [R-CURRENT](#r-current) | Which exact candidate or rule still applies now? | Existing · publication and execution currentness |
| [R-ACCEPTANCE](#r-acceptance) | What does a merged result establish about the promised outcome? | Existing · acceptance and roadmap state |
| [R-EVIDENCE](#r-evidence) | What did the test or report actually establish? | Existing · return evidence and criteria |
| [R-INSTRUCTIONS](#r-instructions) | Which reusable procedure was actually governing the work? | Design · procedure identity/currentness |
| [R-ADOPTION](#r-adoption) | How can a rule change without using its own new rules to adopt itself? | Existing predecessor principle; broader design application |
| [R-ACTIVE-WORK](#r-active-work) | What happens to work halfway through the old procedure? | Existing · execution/publication transition machinery |
| [R-NESTING](#r-nesting) | When does a child plan create useful local independence? | Existing · nesting and references |
| [R-ADVICE](#r-advice) | When can external advice influence a choice without becoming local authority? | Design · external recommendation boundary |
| [R-SHARING](#r-sharing) | Why does resource contribution not transfer governance? | Design · external resource boundary |
| [R-CONTEXT](#r-context) | How can we keep valuable long-lived context without depending on its survival? | Design emphasis supported by recovery records |
| [R-CAPABILITIES](#r-capabilities) | What will cleanup or lifecycle operations actually do on this substrate? | Existing · execution-context capability profiles |
| [R-TRACEABILITY](#r-traceability) | When can a maintainer safely question or remove an old instruction? | Design · rationale backlinks |

The inline **Smell** notes are not operating instructions. They mark places where the attempt to explain the system exposed a reason to come back and challenge it. This foundation intentionally leaves them untriaged; after the guide is accepted they can be connected to design Issues without interrupting the story here.

The narrative and stable-anchor approach follow [Typed Planning's guide][src-tp-guide]. This guide does not adopt its ontology or require NPT to reproduce its classes.

<!-- Exact source references preserve the reviewed foundation baseline. -->

[src-baseline]: https://github.com/davrec72/nested-planning-template/tree/d82b792ba5ad565aba804e72578ff2c88f206caf
[src-agents]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/AGENTS.md
[src-foreman]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/prompts/FOREMAN.md
[src-plan]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/PLAN.md
[src-roles]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/ROLES.md
[src-conventions]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/CONVENTIONS.md
[src-satisfiability]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/SATISFIABILITY.md
[src-nodes]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/NODE_CONTRACTS.md
[src-nesting]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/NESTING.md
[src-references]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/REFERENCES.md
[src-parent]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/PARENT.md
[src-publication]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/PUBLICATION.md
[src-transitions]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/PUBLICATION_TRANSITIONS.md
[src-execution]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/planning/EXECUTION.md
[src-package]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/WORK_PACKAGE.md
[src-inventory]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/EXECUTION_INVENTORY.md
[src-receipt]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/EXECUTION_RECEIPT.md
[src-change]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/PLAN_CHANGE.md
[src-transition-action]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/TRANSITION_ACTION.md
[src-acceptance]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/MILESTONE_ACCEPTANCE.md
[src-child-plan]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/CHILD_PLAN.md
[src-child-roles]: https://github.com/davrec72/nested-planning-template/blob/d82b792ba5ad565aba804e72578ff2c88f206caf/templates/CHILD_ROLES.md
[src-tp-guide]: https://github.com/davrec72/typed-planning/blob/bdfc63d3afbddefaad6c5f732c9e5b38295281b4/docs/guide.md
