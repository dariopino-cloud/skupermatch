# Business process

## Context

Respawn Retail is a fictional online retailer of gaming and technology
accessories.

The current-state description is a business scenario, not an observed
study of a real company. The end-to-end three-app workflow is implemented
in Biscuit.

## Current-state scenario

Supplier lists use inconsistent names and may contain missing attributes
or confusingly similar variants.

Purchasing receives the information. Product Data compares it with the
shop catalogue. E-commerce needs complete and reviewed information
before internal approval.

When clarification happens outside the article context, teams must
manually reconnect answers, product information and decisions.

No quantitative baseline or measured improvement is claimed.

## Target process

| Stage | Owner and app | Action | Handover |
| --- | --- | --- | --- |
| Intake | Purchasing / Supplier Inbox | Create a supplier item | Item becomes available for product-data review |
| Review | Product Data / Match Arena | Select or confirm the candidate shop product and inspect differences | Confirm identity, identify a distinct product or request clarification |
| Clarification | Purchasing / Supplier Inbox | Answer the question and correct information where justified | Answer becomes available to Product Data |
| Resolution | Product Data / Match Arena | Resolve the question and confirm the correct product relationship | E-commerce can review readiness |
| Completion | E-commerce / Launch Board | Complete required information and selling price | Release conditions can be evaluated |
| Internal approval | E-commerce / Launch Board | Approve when all release conditions are satisfied | Product is internally approved, not externally published |

## Product identity

Three distinctions are essential:

1. Multiple suppliers may offer the same canonical shop product.
2. Similar variants are not automatically the same product.
3. A rejected match does not automatically make an item ready for sale.

An incorrect pack-size entry may be corrected after clarification.
A genuine multipack remains a different offer from a single unit.

## Clarification loop

Product Data raises a question linked to the supplier item.
Purchasing answers it and corrects the source information where appropriate.
Product Data reviews the clarification before completing the decision.

Supplier item data cannot be edited freely after creation. Purchasing
can correct it only while answering a clarification question, so every
correction is tied to a documented question and answer.

An answer and a resolved question are different business events:
receiving an answer does not, by itself, establish product identity.

## Internal approval conditions

The business process requires:

- Confirmed matching or confirmed creation of a new shop product.
- Complete required attributes.
- An entered selling price.
- No open clarification question.

Launch Board shows the current blockers as text. Its blocker list is
calculated on each query rather than persisted separately.

## Evaluation and boundaries

The eight-step sequence is documented in the
[demo script](https://github.com/dariopino-cloud/skupermatch/blob/main/docs/demo-script.md).

Not yet tested with separate user accounts.

Internal approval does not upload anything to a real shop.
CSV import and AI suggestions are not in scope for this MVP.
