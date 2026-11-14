# App connections

## Shared architecture

Supplier Inbox, Match Arena and Launch Board use the same Biscuit database.

They are team-specific views and workflows around shared business records,
not three disconnected applications exchanging separate catalogue copies.

## Business responsibilities

The following matrix describes the apps' business responsibilities.
It is not a database permission specification.

| App | Information used | Process contribution |
| --- | --- | --- |
| Supplier Inbox | Supplier offers, clarification questions and review context | Create supplier items, answer questions and correct supplier information where justified |
| Match Arena | Supplier items, candidate shop products and clarification context | Product Data selects or confirms the candidate shop product in Match Arena, reviews discrepancies and resolves matching questions |
| Launch Board | Shop products, matching state, clarification state and current blockers | Complete information, enter selling prices and approve internally |

## How changes become visible

The three apps read and write shared records.

The team observes changes, such as newly created supplier items and
answered questions, appearing in the other apps usually within seconds
without manual refresh.

This is observed behaviour, not a measured latency guarantee or a claim
about Biscuit's underlying synchronization technology.

## Dynamic release blockers

Release blockers in Launch Board are not stored as a separate list.

Each query calculates them from current data and rules. Consequently,
a newly calculated list reflects the information and rules available
at that point rather than an older saved list.

This is an intentional design decision: readiness is evaluated from the
current situation.

On-query calculation and continuous screen updates are different things.
A fresh result requires a new query. The calculation also does not, by
itself, imply automatic withdrawal of a previous internal approval.

## Access and environment

The apps and data live in a private Biscuit workspace.

For authorized users, the team-verified project steps are:

1. Sign in to Biscuit.
2. Open the project workspace.
3. Open Supplier Inbox, Match Arena and Launch Board.
4. Follow the same identifiable item through the workflow.

These are project-specific viewing steps, not a public API, SDK or CLI
integration guide.

There is no local runtime to start and no local environment configuration
required for this workflow.

## Evaluation

The jury sees the private implementation through the live demo and demo
video. There are no public app links.

Follow one supplier item across all three apps and show:

- Its creation in Supplier Inbox.
- Its appearance and review in Match Arena.
- A clarification question returning to Purchasing.
- The answer returning to Product Data.
- The resulting readiness and internal approval in Launch Board.

Not yet tested with separate user accounts.

The responsibilities above should therefore not be treated as evidence
that account-level authorization has been tested across separate users.

See the [demo script](https://github.com/dariopino-cloud/skupermatch/blob/main/docs/demo-script.md).
