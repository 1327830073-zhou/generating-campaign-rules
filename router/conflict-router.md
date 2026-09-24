# Conflict Router

## Base-text conflict
If immutable base text conflicts with explicit user input:
- keep original immutable wording
- append `(纠正：*根据本次玩法，应为“...”*)`
- correction must be directly supported by user input

## Source conflict
If a historical source contains incompatible alternatives:
- mark `SOURCE_CONFLICT`
- do not promote either value to default
- ask for business confirmation if the value is required

## Missing critical info
Never infer business-changing fields. Use `[待确认：字段]` when a draft is still requested.
