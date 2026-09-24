# Blind Tests V1.1

Status legend:
- PASS: current specification directly determines the correct behavior.
- PASS-AFTER-FIX: V1 failed/was ambiguous; V1.1 contains an explicit correction.
- OPEN: needs future corpus or business rule.

## T1 新客定义缺失
Input: “新客累计满599送礼”，没有新客判定口径。
Expected: `[待确认：新客判定口径]`; do not equate to 新会员。
Status: PASS

## T2 误导性运营命名
Input: 做任务得“投票次数”，每3个“投票次数”拆一次盲盒。
Expected: TASK → ACTIVITY_CURRENCY → DRAW(BLIND_BOX), not VOTE.
Status: PASS

## T3 核验上传 vs UGC
Input: 上传订单截图只用于资格审核。
Expected: PRIVATE_PROOF / qualification proof; no PUBLIC_WORK, no ranking.
Status: PASS

## T4 奖品锁定与生效
Input: 下单中奖后锁奖，确认收货7天无售后后生效。
Expected: DRAW → PRIZE_LOCK → ORDER_VALIDATION → EFFECTIVE → ISSUE.
Status: PASS

## T5 参与资格锁权
Input: 预热期报名，正式期才能抽奖。
Expected: PARTICIPATION_RIGHT_LOCK, not PRIZE_LOCK.
Status: PASS

## T6 金额区间阶梯
Input: 0-50返5券，51-120返10券。
Expected: TIERED_REBATE(tier_basis=amount, interval mapping).
Status: PASS

## T7 跨品类阶梯
Input: 跨2类92折，跨3类9折。
Expected: COMBINATION_PURCHASE(CROSS_CATEGORY_BUNDLE) + TIERED_REBATE(category_count).
Status: PASS

## T8 通用底座冲突
Input: 答题结束时发京豆；通用锁定底座写“中奖时直接发放”。
Expected: preserve locked sentence + append correction annotation.
V1 issue: exact locked base sentence was not stored, so exact compliance was impossible.
V1.1 fix: `base/generic-jd-base.md` now stores the exact locked text and fulfillment blocks.
Status: PASS-AFTER-FIX

## T9 单一领奖流程编号
Input: 奖品只有京豆。
Expected: no `①` before the single FLOW_JINGDOU paragraph.
Status: PASS

## T10 综合榜单
Input: 票数60% + 内容质量40%。
Expected: COMPOSITE_SCORE_RANKING with exact weights; do not invent tie-breaker.
Status: PASS

## T11 历史源文件自冲突
Input source: “每日限3次/每日不限次数” simultaneously.
Expected: SOURCE_CONFLICT; do not choose.
Status: PASS

## T12 汤臣倍健企微范围缺失
Input: “需为企微好友”，未说明小汤/小健任一还是两个都要。
Expected: `[待确认：企微好友范围]`.
Status: PASS

## T13 活动值未命名
Input: 完成任务得活动值，每100点抽一次，未命名活动值。
Expected: default to “积分”; do not invent “能量值”.
Status: PASS

## T14 首购 ≠ 新会员
Input: 用户活动期间新入会，但历史上已经购买过商品；规则写“首购礼”。
Expected: do not treat membership join as first purchase without first-purchase definition/history condition.
Status: PASS

## T15 多奖品但单一领取流
Input: 10京豆、50京豆、100京豆。
Expected: one virtual/JINGDOU fulfillment flow; no ①②③ by SKU.
Status: PASS

## T16 美的注意事项锁定
Input: 美的活动，正常使用历史六段结构。
Expected: use MIDEA locked notice text, not a regenerated paraphrase.
V1 issue: brand file contained only a summary, not the exact notice base.
V1.1 fix: exact MIDEA notice base stored in `brands/midea.md`.
Status: PASS-AFTER-FIX

## T17 汤臣倍健活动声明锁定
Input: BYHEALTH standard rule generation.
Expected: use exact three-line activity statement base when applicable.
V1 issue: only a summary was stored.
V1.1 fix: exact activity statement stored in `brands/byhealth.md`.
Status: PASS-AFTER-FIX

## T18 下单角色识别
Input: 下单金额只用于消费排行榜，不直接发奖。
Expected: ORDER → GMV metric → RANKING, not THRESHOLD_REWARD.
Status: PASS

# Self-test summary

V1:
- 15 tests passed by specification.
- 3 tests exposed deployment-blocking gaps: T8, T16, T17.
- Root cause: the skill said some text was “immutable” but did not package the exact immutable source text.

V1.1:
- All 18 specification tests pass on paper after adding the exact locked bases and missing common-atomic reference.
- Remaining limitation: this is a self-test by the same model, not an independent fresh-agent multi-repetition test. The next user-provided unseen activity is therefore the first true external blind test.
