# Question Patterns for Spec Interviews

This reference provides detailed question patterns for each category. Use these as inspiration - adapt them to the specific spec being reviewed.

## 1. Edge Cases & Boundaries

Probe the limits and boundaries of the system:

**Numeric Limits:**
- "The spec mentions [X items]. What happens at X+1? Hard error, soft limit, or degradation?"
- "What's the maximum [size/count/duration] and who decided that number?"
- "What happens if [numeric value] is zero? Negative? Extremely large?"

**Empty/Null States:**
- "What does the UI show when there are no [items] yet? First-run experience?"
- "If [data field] is missing or null, do we use a default, show an error, or hide the element?"
- "What's the experience for a brand new user with no history/data?"

**Timing Boundaries:**
- "What if [action] takes 30 seconds instead of the expected 2 seconds?"
- "Is there a timeout? What happens when it's exceeded?"
- "What if two users do [action] at the exact same millisecond?"

**Format Boundaries:**
- "What characters are allowed in [field]? Unicode? Emoji? RTL text?"
- "What's the max length of [text field] and how is truncation handled?"
- "What file formats are supported and how are unsupported formats rejected?"

## 2. Failure Modes & Error Handling

Explore what happens when things go wrong:

**Partial Failures:**
- "If [operation] partially succeeds (3 of 5 items processed), what state is the user left in?"
- "When [external service] fails mid-transaction, how do we handle the inconsistent state?"
- "If [step 2] fails after [step 1] succeeds, do we rollback step 1 or leave it?"

**Network & Infrastructure:**
- "What happens during a network partition between [service A] and [service B]?"
- "If the database is temporarily unreachable, do we queue operations or fail immediately?"
- "How does the system behave when it comes back up after a crash?"

**User-Caused Failures:**
- "What if the user closes the browser mid-[operation]?"
- "What if they double-click the submit button?"
- "What happens if they navigate away and come back?"

**Recovery Paths:**
- "After [failure], what's the recovery path? Can users retry? Do they need to start over?"
- "Are there idempotency guarantees for [operation]?"
- "What audit trail exists for debugging failures?"

## 3. Implicit Assumptions

Surface hidden assumptions:

**User Assumptions:**
- "The spec assumes users will [behavior]. What if they don't?"
- "This requires users to have [capability/knowledge]. Is that a valid assumption for all users?"
- "What if the user doesn't complete [setup step] that we assume is done?"

**Environmental Assumptions:**
- "This assumes [dependency] is always available. What's the fallback?"
- "The spec assumes [certain data] exists. What if the account is new?"
- "You're assuming [third party] API won't change. What's the contract?"

**Timing Assumptions:**
- "This workflow assumes [action A] happens before [action B]. What enforces that?"
- "The spec assumes near-instant response. What if latency is 5 seconds?"
- "You assume users stay on the page. What about mobile users switching apps?"

**Data Assumptions:**
- "This assumes [data] is always valid/present. Who validates it?"
- "You're assuming [relationship] between data points. Is that always true?"
- "The spec assumes data fits in memory. What's the actual expected size?"

## 4. Tradeoffs & Alternatives

Understand the decisions made:

**Architecture Tradeoffs:**
- "You chose [approach X] over [approach Y]. What drove that decision?"
- "This prioritizes [quality A] over [quality B]. Is that the right tradeoff?"
- "What did you consider and reject? Why?"

**Consistency vs. Availability:**
- "Would you rather have stale data shown or show nothing during [condition]?"
- "Is it acceptable to show optimistic updates that might be rolled back?"
- "Strong consistency here means [latency impact]. Is that okay?"

**Complexity Tradeoffs:**
- "This adds complexity for [edge case]. How often does that actually happen?"
- "Simpler approach would lack [feature]. Is [feature] essential for v1?"
- "Building this flexibility means [cost]. Are we sure we need it?"

**User Experience Tradeoffs:**
- "Faster load time vs. more complete data - which wins?"
- "Simpler UI vs. power user features - who are we optimizing for?"
- "Inline editing vs. modal - what's the rationale?"

## 5. State & Data

Clarify data flows and state management:

**State Transitions:**
- "What are all the valid states for [entity]? Can you draw the state machine?"
- "What triggers the transition from [state A] to [state B]?"
- "Can [entity] ever go backwards in its state lifecycle?"

**Data Ownership:**
- "Who owns [data]? What happens when [owner] is deleted?"
- "If [entity A] references [entity B] and B is deleted, what happens to A?"
- "Is this data denormalized? What's the source of truth?"

**Concurrency:**
- "Two users editing [same resource] - last write wins, merge, or lock?"
- "What's the conflict resolution strategy for [operation]?"
- "Is eventual consistency acceptable for [data], or do we need strong consistency?"

**Data Lifecycle:**
- "When is [data] created? By whom? Through what action?"
- "How long is [data] retained? Is there a deletion policy?"
- "What triggers recalculation of [derived data]?"

## 6. User Experience

Drill into the actual user journey:

**Flow Interruptions:**
- "What if the user abandons the flow at step 3 of 5? What state are they in when they return?"
- "Back button pressed during [operation] - what happens?"
- "User refreshes the page during [process] - expected behavior?"

**Feedback & Communication:**
- "How does the user know [operation] succeeded? What's the confirmation?"
- "What loading states exist? Skeleton, spinner, or optimistic?"
- "How are errors communicated? Inline, toast, modal, page-level?"

**Progressive Disclosure:**
- "What does a new user see vs. an experienced user?"
- "Are there feature gates or progressive unlock of capabilities?"
- "How much information is shown by default vs. on expansion?"

**Accessibility & Inclusivity:**
- "How does this work with screen readers?"
- "What about users with slow internet connections?"
- "Does this work on mobile? Tablet? Differently-abled users?"

## 7. Security & Privacy

Probe security implications:

**Access Control:**
- "Who can see [data]? Who can modify it? Who can delete it?"
- "If permissions change, what happens to existing [resources]?"
- "What prevents user A from accessing user B's [resource]?"

**Attack Vectors:**
- "What if someone submits [malicious input] in [field]?"
- "Rate limiting on [endpoint]? What are the limits?"
- "What prevents automated abuse of [feature]?"

**Data Sensitivity:**
- "Is [data] considered PII? What's the handling policy?"
- "What's logged? Could logs contain sensitive data?"
- "How is [sensitive data] encrypted at rest/in transit?"

**Audit & Compliance:**
- "What actions need audit trails?"
- "Who can access audit logs?"
- "Retention requirements for [data type]?"

## 8. Performance & Scale

Explore scaling characteristics:

**Load Characteristics:**
- "What's the expected read/write ratio for [operation]?"
- "Peak load vs. average load - what's the multiplier?"
- "Are there predictable traffic patterns (time of day, day of week)?"

**Resource Consumption:**
- "What's the memory footprint per [operation/user/request]?"
- "Database queries per [action] - is that bounded?"
- "File storage growth rate - what's the projection?"

**Degradation Strategy:**
- "At 80% capacity, what degrades first?"
- "Is there a circuit breaker for [dependency]?"
- "What's the graceful degradation path?"

**Caching Strategy:**
- "What's cacheable? What cache invalidation strategy?"
- "Cache miss scenario - what's the user experience?"
- "Stale cache acceptable? For how long?"

## 9. Integration & Dependencies

Understand external touchpoints:

**External Services:**
- "What's the SLA for [external dependency]? What if they miss it?"
- "API versioning strategy for [integration]?"
- "What data do we send to [third party]? Privacy implications?"

**Internal Services:**
- "What other teams/services does this affect?"
- "Who needs to be notified about changes?"
- "What's the deployment coordination needed?"

**Data Exchange:**
- "Import from [source] - format, validation, error handling?"
- "Export to [destination] - format, scheduling, failure handling?"
- "Webhook delivery - retry policy, ordering guarantees?"

## 10. Evolution & Maintenance

Think about the future:

**Versioning:**
- "How do we handle breaking changes to [API/schema/format]?"
- "Migration path for existing [users/data] when we add [feature]?"
- "Can old clients coexist with new ones?"

**Feature Flags & Rollout:**
- "Gradual rollout strategy for [feature]?"
- "Kill switch if [feature] causes problems?"
- "A/B testing considerations?"

**Technical Debt:**
- "Known shortcuts we're taking that need revisiting?"
- "What's hardcoded that should be configurable?"
- "What documentation needs to exist before handoff?"

**Observability:**
- "What metrics indicate this feature is healthy?"
- "What alerts should fire and when?"
- "How do we debug [scenario] in production?"

## Interview Pacing

**First Round:** Start with 2-3 questions about the most critical unknowns - usually edge cases or failure modes that could sink the project.

**Middle Rounds:** Explore systematically across categories, grouping related questions. Use multi-select for preference-style questions.

**Final Rounds:** Focus on integration, evolution, and any threads that emerged from earlier answers.

**Wrap-up:** Confirm the most important decisions, note any remaining open questions, and verify the user feels the critical gaps are addressed.
