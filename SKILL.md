---
name: generating-campaign-rules
description: Use when users need to draft, complete, rewrite, or check JD-style promotional activity rules involving quizzes, tasks, points, draws, UGC, rankings, invitations, orders, first purchase, repurchase, threshold rewards, tiered rebates, combination purchases, brand-specific rule bases, prize fulfillment, or mixed campaign mechanics.
---

# Generating Campaign Rules

## Overview

Generate activity rules by routing the user's brief into reusable atomic mechanics, then composing those mechanics under the correct brand/base structure.

**Core principle:** do not search for a whole historical campaign template first. Decompose the request into atomic mechanics, variants, gates, reward flows, and brand-specific immutable text, then recombine them.

Historical cases are evidence for rules; they are not copy targets.

## Required execution order

1. Parse user input.
2. Route brand.
3. Identify participant/user segment.
4. Decompose into atomic mechanics.
5. Select variants.
6. Build mechanic dependency graph in actual user journey order.
7. Apply gates/validation.
8. Apply reward type and fulfillment flow.
9. Load brand/base immutable text.
10. Run conflict and missing-information checks.
11. Generate final rules.

## Input handling

Extract when present:

- brand/category
- activity time
- participating stores
- participant eligibility
- membership/WeCom requirement
- product scope
- mechanics
- core logic
- activity-value name
- thresholds, limits, periods
- reward list and reward type
- order validation/effectiveness conditions
- special fulfillment rules

If an activity value is required but the user did not name it, use **“积分”**. Never invent names such as 能量值、活力值、焕新值.

Do not invent missing numbers, dates, limits, thresholds, ranking weights, user-segment definitions, or order-validity rules.

## Brand routing

Brand rules override the generic structure when a supported brand base exists.

Supported brand bases in V1:
- `MIDEA`
- `BYHEALTH`

Otherwise use the generic JD structure.

See `router/brand-router.md`.

## Mechanic routing

Prefer existing atomic mechanics. Create a new top-level mechanic only when the request cannot be faithfully expressed using existing mechanics plus variants.

Atomic mechanics in V1:
- TASK
- CHECK_IN
- INVITE
- ORDER
- UGC_UPLOAD
- CONTENT_VIEW
- INTERACTIVE_CONTENT
- QUIZ
- DRAW
- ENGAGEMENT
- RANKING
- FIRST_PURCHASE
- REPURCHASE
- THRESHOLD_REWARD
- TIERED_REBATE
- COMBINATION_PURCHASE
- PARTICIPATION_RIGHT_LOCK
- ACTIVITY_CURRENCY
- DRAW_CHANCE
- PRIZE_LOCK

Gates:
- CONTENT_REVIEW
- ORDER_VALIDATION

See `router/mechanic-router.md` and `mechanics/common-atomic.md`.

## Hard routing rules

1. Route by behavior, not by marketing label.
   - A field called “投票次数” may actually behave as an activity currency if users consume it to draw prizes.
2. An upload must first be classified by purpose:
   - proof/verification
   - public work
   - text UGC
   - external social post
   - claim material
3. An order must first be classified by role:
   - participation condition
   - draw-chance source
   - ranking metric
   - reward trigger
   - reward-effectiveness prerequisite
   - activity-currency source
4. Distinguish:
   - new member
   - new customer
   - first-purchase user
   - returning customer
   - repurchase stage
5. “新客/老客” without a definition is `MISSING_CRITICAL_INFO`; do not equate it to membership status.
6. Distinguish single-order amount from cumulative amount.
7. Distinguish tier types:
   - cumulative threshold
   - mutually exclusive tiers
   - interval mapping
   - category-count / quantity / order-count tiers
8. Distinguish participation-right lock from prize lock.
9. Prize locked ≠ prize effective ≠ prize issued.
10. “确认收货X天无售后” is an **effectiveness condition** for a locked reward.
11. Historical-source conflicts must be surfaced as `SOURCE_CONFLICT`; never silently choose one value.
12. User input conflicting with immutable base text:
   - keep the base text
   - append `(纠正：*...*)` using only explicit user-provided information.

## Quiz

Use only these confirmed variants in V1:
- QUIZ-A fixed question set / pass threshold
- QUIZ-B daily unlock / cumulative correct count
- QUIZ-C continuous answering / wrong answer clears current round
- QUIZ-D ordinary per-question judgment

For detailed rules see `mechanics/quiz.md`.

## UGC and ranking

UGC variants:
- PRIVATE_PROOF
- PUBLIC_WORK
- TEXT_UGC
- EXTERNAL_SOCIAL_POST

Engagement variants:
- VOTE
- LIKE
- EXTERNAL_HEAT

Ranking variants:
- POINTS_RANKING
- VOTE_RANKING
- LIKE_RANKING
- EXTERNAL_HEAT_RANKING
- GMV_RANKING
- COMPOSITE_SCORE_RANKING

Keep ENGAGEMENT separate from RANKING:
engagement produces the metric; ranking consumes it.

See `mechanics/ugc-ranking.md`.

## Purchase domain

Purchase mechanics:
- ORDER
- FIRST_PURCHASE
- REPURCHASE
- THRESHOLD_REWARD
- TIERED_REBATE
- COMBINATION_PURCHASE

Purchase-lifecycle states may be modeled as:
`NO_PURCHASE → FIRST_PURCHASED → REPURCHASE_1 → REPURCHASE_2 → ...`

See `mechanics/purchase.md`.

## Order validation

Use the state model:

`reward/prize condition met → prize qualification locked → linked order → order received + X days with no after-sales → reward effective → issue/claim`

Do not represent “售后观察期” as a separate peer mechanic.

See `gates/order-validation.md`.

## Prize fulfillment

Choose a fulfillment flow by reward type, not by SKU count.

Supported flows:
- VIRTUAL_AUTO_ISSUE
- PHYSICAL_ADDRESS_FULFILLMENT
- PHYSICAL_PRIZE_VIA_COUPON_ORDER
- MANUAL_CLAIM

If only one fulfillment flow exists under “奖品领取流程”, do not prefix it with `①`.
Use `①②③` only when 2+ distinct fulfillment flows are needed.

See `rewards/fulfillment.md`.

## Generic JD immutable base

For generic JD-style rules use:

1. 活动时间
2. 参与条件
3. 活动玩法
4. 领奖须知
5. 其他活动细则

Sections 4 and 5 are immutable-base text except:
- date variables
- section 4.1 fulfillment-flow routing
- explicit conflict annotations

The exact locked text and supported fulfillment blocks are stored in `base/generic-jd-base.md`.
Do not generate these sections from memory or summarize them.

Do not “improve” wording, punctuation, subject, legal phrasing, or platform terms.

See `base/generic-jd-base.md`.

## Brand bases

### MIDEA
Prefer:
1. 活动时间
2. 本活动参与店铺
3. 参与对象
4. 玩法细则
5. 活动玩法发奖规则
6. 注意事项

Use the current activity's explicit store input over brand defaults.

See `brands/midea.md`.

### BYHEALTH
Route WeCom friend requirement, product scope, order linking, reward invalidation, and nutritionist fallback.

See `brands/byhealth.md`.

## Source-conflict handling

When the source itself contains mutually incompatible values:
- do not normalize
- do not choose one
- mark the field as `SOURCE_CONFLICT`
- require user/business confirmation before treating it as a reusable rule

## Missing-information handling

Two classes:

### Safe to default
- unnamed activity value → “积分”

### Must not infer
Examples:
- new/old customer definition
- ranking weights
- vote limits
- order-validity window
- confirmation/receipt days
- refund/after-sales behavior
- payout deadline
- store/product eligibility where it materially changes participation

Use `[待确认：...]` in draft output if the user wants a draft before confirming.

## Output shaping

For final activity rules:
- write in actual participant journey order
- one mechanism point per rule item where possible
- separate base reward from milestone bonus
- separate normal failure from abnormal exit
- separate eligibility lock from prize lock
- separate prize effectiveness from prize issuance

Do not expose internal route names unless the user asks for the reasoning/spec.

## Final checks

Before output verify:
- correct brand structure loaded
- all user-supplied mechanics preserved
- no invented thresholds/limits/weights
- correct single vs cumulative order logic
- correct new-member/new-customer/first-purchase/repurchase logic
- correct tier type
- correct upload purpose
- correct ranking metric and tie-breaker source
- correct prize-lock/effectiveness/issuance flow
- correct number of prize-fulfillment flow indices
- immutable text unchanged except allowed substitutions/annotations
- source conflicts and missing critical fields surfaced
