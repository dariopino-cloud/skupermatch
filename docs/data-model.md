# Shared data model

Attribute names are conceptual; exact field names in the Biscuit
workspace may differ.

This document describes the business entities and relationships of the
shared model. The types below describe business values rather than
Biscuit-specific storage types. It is not a schema export or import template.

## Entities

| Entity | Conceptual attributes and types | Relationships |
| --- | --- | --- |
| Supplier | Supplier identifier (identifier), supplier name (text) | One supplier has multiple supplier items |
| SupplierItem | Item identifier (identifier), supplier (reference), supplier SKU (text), title (text), brand (text), model (text), variant (text), GTIN (text), category (category), pack size (whole-number quantity), purchase price (money), description (text), review state (state) | Belongs to a supplier; participates in matching and clarification |
| ShopItem | Product identifier (identifier), canonical title (text), brand (text), model (text), variant (text), GTIN (text), category (category), pack size (whole-number quantity), description (text), selling price (money), internal approval state (state) | Represents the canonical shop product; may be offered by multiple supplier items |
| MatchProposal | Proposal identifier (identifier), supplier item (reference), candidate shop product where applicable (reference), proposed or confirmed relationship (state), explanation (text) | Connects supplier-item review with a candidate or confirmed shop product |
| Query | Question identifier (identifier), supplier item (reference), question (text), answer (text), clarification state (state) | Carries the clarification loop between Product Data and Purchasing |
| DecisionLog | Entry identifier (identifier), affected item or proposal (reference), decision or correction (text/state), explanation (text), decision time (timestamp) | Represents the timestamped decision history |

## Relationship structure

- A Supplier can have many SupplierItems.
- Several SupplierItems may represent offers for the same ShopItem.
- A MatchProposal relates a supplier item to a candidate product and
  records the business decision about that relationship.
- A candidate relationship is not automatically a confirmed match.
- Queries preserve clarification in the context of the supplier item.
- DecisionLog represents decision history rather than another copy
  of the product catalogue.

The model distinguishes proposed and confirmed relationships without
requiring a separate public table definition for each.

## Product identity rules

### Multiple suppliers, one canonical product

Different supplier offers can refer to the same canonical ShopItem.
Supplier identity or supplier SKU alone does not require creating a
duplicate shop product.

### Similar variants remain distinct

A similar title does not prove identity. Differences such as variant
or pack size must be reviewed before confirming a match.

### Rejection is not approval

Rejecting a candidate only rejects that relationship.
It does not automatically establish another match, create a complete
new product or approve an item for sale.

## Internal approval checklist

All four business conditions are required:

1. Matching or new-product creation is confirmed.
2. Required product attributes are complete.
3. A selling price is entered.
4. No clarification question remains open.

The conceptual product attributes above describe the information involved
in the workflow. Their presence in this document does not assert a
particular database constraint for every attribute.

## Approval state and derived blockers

Internal approval is a business state.

The Launch Board blocker list is derived from current data and rules on
every query. It is not stored as a separate list or model entity.

This design avoids an outdated saved blocker list. It does not, by itself,
establish automatic revocation of a previously approved item.

## Corrections and history

The intended decision-history model distinguishes a product relationship
from the decision that established or corrected it.

A decision log must not be described as a complete audit trail for every
direct field edit unless that wider coverage has been established.
