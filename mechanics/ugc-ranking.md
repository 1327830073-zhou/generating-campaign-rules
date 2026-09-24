# UGC and Ranking

## UGC variants
- PRIVATE_PROOF: content used only for verification; may require privacy/retention text.
- PUBLIC_WORK: public competition work.
- TEXT_UGC: comment/message/text entry.
- EXTERNAL_SOCIAL_POST: post on external social platform.

Common fields:
- content_type
- submission_limit
- resubmit_allowed
- category/track
- content_requirement
- device/watermark requirement
- visibility
- review_required
- platform
- image_min
- text_min
- required_topics
- originality_requirement

## CONTENT_REVIEW
A gate controlling one or more:
- display
- participation validity
- reward
- ranking eligibility

## ENGAGEMENT
- VOTE
- LIKE
- EXTERNAL_HEAT

## RANKING
Variants:
- POINTS_RANKING
- VOTE_RANKING
- LIKE_RANKING
- EXTERNAL_HEAT_RANKING
- GMV_RANKING
- COMPOSITE_SCORE_RANKING

Fields:
- ranking_metric
- metric_source
- ranking_formula
- eligibility
- update_mode
- lock_time
- publish_time
- top_n
- reward_tiers
- tie_breaker
- invalid_data_rule

Never invent composite weights or social-heat weights.
