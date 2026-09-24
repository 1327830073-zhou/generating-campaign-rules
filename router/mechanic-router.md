# Mechanic Router

## Recognition rule
Identify what the user does, what state/value it produces, and what consumes that state/value.

## Typical graphs

TASK → ACTIVITY_CURRENCY → DRAW
TASK → DRAW_CHANCE → DRAW
UGC_UPLOAD → CONTENT_REVIEW → ENGAGEMENT → RANKING → REWARD
ORDER → DRAW_CHANCE → DRAW → PRIZE_LOCK → ORDER_VALIDATION → REWARD
FIRST_PURCHASE → THRESHOLD_REWARD → ORDER_VALIDATION → REWARD
REPURCHASE_N → THRESHOLD_REWARD → ORDER_VALIDATION → REWARD
COMBINATION_PURCHASE → TIERED_REBATE → PRIZE_LOCK → ORDER_VALIDATION → REWARD
PARTICIPATION_RIGHT_LOCK → future participation window → DRAW

## Decision guards

- “上传” → classify purpose before UGC.
- “下单” → classify role before choosing order mechanic.
- “投票次数” → classify by use, not name.
- “阶梯” → classify cumulative / mutually exclusive / interval / category-count / quantity / order-count.
- “锁权” → determine whether it locks future participation or a prize.
