# Generic JD Base

Use this structure when no brand-specific base applies:

一、活动时间
二、参与条件
三、活动玩法
四、领奖须知
五、其他活动细则

# Locked Section 4/5 Contract

Sections 四 and 五 are source-locked text.

Allowed changes only:
1. Replace date variables.
2. In 四-1, select the fulfillment block(s) matching the reward type.
3. If explicit current-user input conflicts with locked text, preserve the locked text and append:
   `（纠正：*根据本次玩法，应为“...”*）`

Do not paraphrase, shorten, optimize, fix punctuation, replace subjects, or silently correct wording.

# 四、领奖须知

## 1、奖品领取流程：

Select only the flow blocks needed for the current reward set.

### FLOW_JINGDOU

用户活动中获得的京豆，将于中奖时直接发放至京东账户中，如未到账可能是延迟原因导致，如 24 小时未到账请咨询京东在线客服。

### FLOW_GENERIC_VIRTUAL

用户活动中获得的虚拟奖品（优惠劵、京豆、积分）将于中奖时直接发放至京东账户中，如未到账可能是延迟原因导致，如 24 小时未到账请咨询京东在线客服。

### FLOW_PHYSICAL

用户获得实物礼品，可在弹窗中领取并填写收货信息，若用户在领取奖品过程中，因手机故障或其他原因中止退出程序，可于活动结束前到「我的奖品」按钮中重新填写信息，填写后无法更换信息，请仔细填写！最晚不超过 {ADDRESS_DEADLINE}；如未在规定时效内完成填写，将视作自动放弃奖品。

用户活动中获得的实物奖品，活动结束后将由店铺客服核实用户中奖资格，奖品将于 {SHIP_DEADLINE} 前陆续发货，请耐心等待；

*实物奖品不可叠加领取，一个 ID 只能领取一份

### FLOW_COUPON

用户活动中获得的优惠券将于中奖时直接发放至账户中，点击【去使用】可跳转活动商品页面使用，如未到账可能是延迟原因导致，如 24 小时未到账请咨询店铺在线客服。

## Numbering

- If exactly one fulfillment flow is used, output its text directly with no `①`.
- If 2+ distinct fulfillment flows are used, number the selected flows `①②③...`.
- Count fulfillment flow types, not prize SKUs.

## 2、奖品领取说明：

①每位自然人用户仅能使用同一个账号参与活动，京东账号、收货地址、手机号码等任意信息一致或指向同一用户，则视为同一用户；第一个参与本活动的账号参与结果有效，其他账号参与本活动均视为无效，若发现同一用户使用不同账号重复参与活动，商家有权取消其获奖资格。

②本活动的所有奖品仅限中奖人本人领取，不得转让、转售、折现或兑换任何其他实物或权益，也不能用作其他商业用途。

# 五、其他活动细则：

1、活动期间，若出现参与者通过不正当手段、不诚信方式参与活动的（包括但不限于机器作弊、恶意套取、刷信誉、虚假交易、扰乱系统、实施网络攻击等），本店铺有权单方面取消其抽奖参与资格及所获奖品；若奖品已发出的，本店铺有权要求中奖者退回奖品，或在中奖者拒绝或无法退回奖品的情况下在向中奖者的退款（如有）中扣除奖品价值。

2、所有奖品仅限中奖者本人领取。主办方有权在任何时候对中奖者的中奖资格进行复核。如中奖者存在任何不再符合中奖条件的情形（包括但不限于中奖者的订单发生仅退款/退货退款等导致中奖者不再符合获取中奖资格的前提条件），均视为其主动放弃相应的抽奖参与资格及奖品，主办方有权不予提供奖品。

3、如遇不可抗力、政府管制（包括但不限于重大灾害事件、活动受政府机关指令需要停止举办或调整的等）、网络传输故障、系统发生故障或遭受第三方攻击及其他主办方无法控制的情形，在法律允许的范围内主办方对前述情形所导致的一切后果不承担任何责任，并有权相应地取消、终止、修改、暂停或延迟本次活动。

4、本店铺可以根据本活动的实际举办情况对活动规则进行变动或调整，相关变动或调整将公布在活动页面上，公布后依法生效。

5、若您对活动有任何疑问，请在 {START_TIME}（活动开始时间）-{END_PLUS_7_DAYS}（活动结束后 7 日）内咨询参与活动店铺在线客服，过期将不予处理。

6、用户单品购买 5 件以上，全品购买 15 件以上，且都为同一收货地址，视为集体采购，不参与活动。如有疑义，可联系客服，核实无误后可补领权益。京东帮及专卖店账号不参与活动，类似批发下单同一账号的经销商、批发商用户也均不参与。

7、如对本次活动有任何其他问题，请详询京东在线客服。
