# NLTC Experiment Function Refactor

## Summary
Created a dedicated `NLTC_experiment()` function to handle Natural Language to Command experiment conditions (9-11), separating it from the shared `whFunction()` logic.

## Changes Made

### 1. Added NLTC Variables (lines 2527-2530)
```javascript
var nltc_questions = ['I think Berth1 is blocked. Where do you want me to put this bag?',
                      'I think Berth2 is blocked. Where do you want me to put this bag?'];
var ne_nltc=0;
var nltcclear;
```

### 2. Created NLTC_experiment() Function (lines 3280-3550)
- Modeled after `whFunction()` but with NLTC-specific logic
- Always displays text box input (no button mode toggle)
- Records trial data with 'nltc_' phase prefixes to distinguish from wh mode
- Handles all three berth combinations (Berth 1 blocked, Berth 2 blocked)
- Manages click handlers for berth selection
- Uses `nltcclear` timeout to avoid handler stacking

Key features:
- Video display for blocked berth scenarios
- Reward logic based on user actions:
  - Valid action: Reward +50
  - Valid medium: Reward +30
  - Invalid action: Reward -100
- 25-second timeout before automatic robot action

### 3. Added Condition Routing (lines 4461-4506)
Added handling for conditions 9, 10, and 11:
```javascript
if (condition==9)  { NLTC_experiment(); sawareness_NLTC(); ... }
if (condition==10) { NLTC_experiment(); sawareness_NLTC(); ... }
if (condition==11) { NLTC_experiment(); sawareness_NLTC(); ... }
```

Each condition:
- Calls `NLTC_experiment()` initially
- Sets up recurring interval calls every 80 seconds
- Uses `sawareness_NLTC()` for NLTC-specific situation awareness checks
- Clears previous condition timeouts

## Experiment Design Integration
- Conditions 9-11 correspond to the same n-back difficulty levels as conditions 3-5:
  - Condition 9: 0-back (same as condition 3)
  - Condition 10: 1-back (same as condition 4)
  - Condition 11: 2-back (same as condition 5)
- All three NLTC conditions use text input (natural language) instead of button selection
- Shares the same `/natural_lang_to_command` API endpoint for LLM processing

## Data Recording
NLTC trial data uses NLTC-specific phase names:
- `NLTC_question`: The question asked by the robot
- `NLTC_video_shown`: Which berth was shown as blocked in the video
- `NLTC_put_bag`: Which action element was shown after user input
- `user_NLTC`: Classification of user action (valid/invalid/valid medium)
- `Reward_NLTC`: Reward given to participant
- `NLTC_user_text`: The text input provided by the user

Neither the WH nor NLTC experiment logs an input-mode phase.

## Backward Compatibility
- Original conditions 0-8 unchanged
- `whFunction()` still used for conditions 3-5
- Existing `/natural_lang_to_command` API endpoint still used for NLTC text processing
- Text box UI elements (#wh_input, #wh_send, etc.) reused by both wh and NLTC modes
