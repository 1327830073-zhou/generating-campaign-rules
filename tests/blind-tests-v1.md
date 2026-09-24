# Blind Test Scenarios for V1

These are deployment tests; V1 should not be treated as fully verified until it passes them.

## T1 New customer ambiguity
Input uses “新客满额” without defining new customer.
Expected: mark new-customer definition as missing; do not equate to new member.

## T2 Misleading variable name
Tasks grant “投票次数”; 3 投票次数 are consumed per blind-box draw.
Expected: route as ACTIVITY_CURRENCY → DRAW, not VOTE.

## T3 Upload proof vs public UGC
User uploads a receipt/photo only for qualification review.
Expected: PRIVATE_PROOF or claim material; no public UGC/ranking assumptions.

## T4 Prize lock
User wins after order, reward is locked, becomes valid after confirmed receipt 7 days with no after-sales.
Expected: PRIZE_LOCK → ORDER_VALIDATION → effective → issue.

## T5 Participation lock
User signs up during warm-up and can draw only after launch time.
Expected: PARTICIPATION_RIGHT_LOCK, not PRIZE_LOCK.

## T6 Tier classification
Single-order amount 0-50 gets 5 coupon, 51-120 gets 10 coupon.
Expected: TIERED_REBATE interval mapping, not cumulative threshold.

## T7 Category tier
Cross 2 categories 92折, cross 3 categories 9折.
Expected: TIERED_REBATE category_count + COMBINATION_PURCHASE.

## T8 Generic base conflict
User explicitly says quiz reward issues when ending quiz; immutable generic base says “中奖时”.
Expected: preserve base sentence and append correction annotation.

## T9 Single fulfillment flow
Only 京豆 prize.
Expected: no `①` before the only fulfillment-flow paragraph.

## T10 Composite ranking
User provides vote 60% + quality 40%.
Expected: COMPOSITE_SCORE_RANKING with exact weights; no invented tie-breaker.

## T11 Historical source conflict
Source contains “每日限3次/每日不限次数”.
Expected: SOURCE_CONFLICT; do not choose either as default.

## T12 BYHEALTH WeCom ambiguity
Brand is 汤臣倍健, user says “需要企微好友” but does not say one or both.
Expected: ask/mark missing one-vs-both requirement.
