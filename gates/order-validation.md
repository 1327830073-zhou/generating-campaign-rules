# Order Validation

Model order-bound rewards as states:

1. reward/prize condition met
2. prize qualification locked
3. link qualifying order
4. order reaches required receipt state
5. required X days pass with no disqualifying after-sales
6. reward becomes effective
7. reward is issued or becomes claimable

Fields:
- lock_trigger
- linked_order
- effective_after_receipt_days
- invalidating_events
- reward_effective
- reward_issue
- chance_restore

Possible invalidating events:
- cancellation
- refund
- return
- other after-sales event explicitly defined by user/source

Do not create a separate “售后观察期” mechanic.
“确认收货X天无售后” is the condition that moves a locked reward into effective state.
