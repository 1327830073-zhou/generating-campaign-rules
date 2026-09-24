# Purchase Domain

## ORDER
Fields:
- store_scope
- product_scope
- amount_basis
- amount_threshold
- quantity_condition
- payment_required
- receipt_required
- order_period
- daily_limit
- total_limit
- quantity_to_chance_mapping

## USER PURCHASE SEGMENT
Keep distinct:
- NEW_MEMBER
- NEW_CUSTOMER
- FIRST_PURCHASE_USER
- RETURNING_CUSTOMER
- REPURCHASE_STAGE_N

Do not equate customer status to membership status without an explicit definition.

## FIRST_PURCHASE
Fields:
- identity_basis
- lookback_cutoff
- membership_required
- store_scope
- amount_threshold
- validation_rule

## REPURCHASE
Fields:
- purchase_sequence
- base_event
- time_window
- amount_threshold
- reward
- validation_rule

## THRESHOLD_REWARD
Fields:
- amount_basis: single / cumulative
- threshold
- segment
- reward
- claim_type
- validation
- limit

Variants:
- ordinary threshold
- mutually exclusive tiers

## TIERED_REBATE
Fields:
- tier_basis: amount / category_count / quantity / order_count
- tiers
- stackable
- frequency
- unlock_rule

## COMBINATION_PURCHASE
Variants:
- MULTI_GROUP_BUNDLE
- CROSS_CATEGORY_BUNDLE

Fields:
- participating groups/categories
- min each group
- quantity matching
- category count
- amount rule
- downstream reward
