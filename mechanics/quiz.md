# Quiz

Confirmed V1 variants only.

## QUIZ-A Fixed set / pass threshold
Fields:
- question_count
- pass_count
- attempt_limit
- exit_reset

## QUIZ-B Daily unlock / cumulative
Fields:
- daily_question_count
- cumulative_correct_count
- milestone_rewards
- cross_day_accumulation

## QUIZ-C Continuous / clear-on-wrong
Recommended output order:
1. 获取答题机会
2. 答题得分规则
3. 阶梯打卡额外奖
4. 结算与清零机制
5. 异常说明

Fields:
- chance_source
- base_reward_per_correct
- milestones
- wrong_action
- manual_end_action
- abnormal_exit_action

## QUIZ-D Ordinary per-question
Use when no confirmed special round/milestone/clear mechanics exist.

Never invent question count, pass threshold, time limit, or attempt count.
