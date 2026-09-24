# Common Atomic Mechanics

## TASK
A user completes a defined action. TASK may produce:
- ACTIVITY_CURRENCY
- DRAW_CHANCE
- RANKING metric
- direct reward

Do not assume a task's output.

## CHECK_IN
Variants:
- daily check-in
- continuous streak
- staged milestones
- check-in with proof upload

Fields:
- cadence
- streak behavior
- reset_on_break
- milestone rewards
- proof requirement

## INVITE
Variants:
- invite entry
- invite + required friend action
- assist
- new-user invite

Fields:
- inviter condition
- invitee condition
- required invitee action
- per-day / total cap
- self-invite prohibition if explicitly provided

## ACTIVITY_CURRENCY
An intermediate consumable/accumulable activity value.

If user gives a name, preserve it.
If no name is supplied, use “积分”.
Never invent a branded activity-value name.

## DRAW_CHANCE
A non-monetary participation count consumed by a DRAW.
Track source, cap, expiration, and source-consumption priority when provided.

## DRAW
Variants:
- LOTTERY
- SCRATCH_CARD
- WHEEL
- BLIND_BOX
- OTHER_RANDOM

Do not infer probability, guaranteed-win status, or inventory.

## PARTICIPATION_RIGHT_LOCK
Locks future eligibility before the main participation window.
Typical graph:
报名/预约 → 锁定参与资格 → 到指定时间 → 抽奖/抢购/领取

## PRIZE_LOCK
Locks a reward qualification after a win/threshold.
PRIZE_LOCK must be followed by the actual effectiveness condition if one exists.
