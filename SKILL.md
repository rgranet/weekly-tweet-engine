---
name: weekly-tweet-engine
description: >
  Generate a week of strategic tweets for indie dev / build-in-public accounts.
  Triggers on: "generate tweets", "batch tweets", "weekly tweets", "plan my week on X",
  "tweet about [topic]", "I need content for this week", or any request to produce
  Twitter/X content in batch. Also triggers when user shares a trend, milestone, or
  launch and wants to turn it into tweets. Works alongside coreyhaines31/marketingskills
  social-content skill if installed.
compatibility: claude-code, cursor, codex
---

# Weekly Tweet Engine

Batch-generate a week of power-law-optimized tweets in ~15 minutes.

---

## Quick start (copy-paste into Claude Code or Cursor)

### First time setup
```
Read the skill at .claude/skills/weekly-tweet-engine/SKILL.md.
Then ask me a few questions to create my tweet profile at tweets/profile.md.
Keep it short — just my projects, voice, and schedule.
```

### Weekly batch (every Sunday)
```
Read tweets/profile.md and the skill at .claude/skills/weekly-tweet-engine/SKILL.md.
Run the weekly review first (ask me about last week's performance).
Then generate my tweets for this week:

- This week I [what happened: milestones, launches, bugs, stats]
- Trends I spotted: [any viral thing, or "none, find some"]
- Focus project: [which project gets the power bets]
```

### Quick mid-week generation
```
Read tweets/profile.md. Write 3 tweets about [topic/trend/milestone].
Use the hook formulas from the tweet engine skill.
```

### After a tweet performs well
```
Read tweets/profile.md. My tweet about [topic] got [X impressions / Y likes].
Run the outlier protocol: generate follow-up thread + Reddit cross-post + series plan.
```

---

## Profile setup

On first run, create `tweets/profile.md` by asking the user these questions.
Keep the file SHORT — under 40 lines. It should be easy to update when projects change.

```markdown
# Tweet profile

## Me
- Name:
- X handle:
- One-line bio:

## Projects (ranked by current Twitter priority)
1. [Name] — [one-liner]
2. [Name] — [one-liner]
3. ...

## Content pillars
| Pillar | ~% | What kind of content |
|--------|----|----------------------|
| [e.g. Build in public] | 30% | [e.g. Code, screenshots, stats] |
| [e.g. Educational] | 25% | [e.g. Frameworks, how-tos] |
| ...    |    |                      |

## Voice
- Tone: [e.g. direct, technical but accessible, slightly irreverent]
- Never say: [e.g. "game-changer", "buckle up", "let that sink in"]
- Hashtags: [2-3 sets by context, e.g. #buildinpublic #indiedev for BIP]

## Schedule
- Days active: [e.g. Mon-Sat]
- Tweets/day: [e.g. 3-5]
- Time budget: [e.g. 30 min/day]
- Best posting time: [e.g. 9-11am local]
- Power bet day: [e.g. Wednesday]
```

**Important:** This profile should evolve. If the user pivots (new project, new focus), update it. Don't generate tweets about projects the user is no longer actively pushing.

---

## How to generate

### Step 0 — Weekly review (always runs first)

Before generating new tweets, review last week's performance. This builds the log automatically.

**If `tweets/log.md` exists**, read it to know past patterns.

**Then ask the user these 4 questions** (quick-fire, should take 60 seconds):

1. "What was your best tweet this week? (paste it or describe it)"
2. "Rough numbers? (impressions, likes, or just 'did well' / 'flopped')"
3. "Follower count now? (so I can track the delta)"
4. "Anything you posted that surprised you — good or bad?"

**Then auto-append to `tweets/log.md`:**

```markdown
## Week of [last Monday's date]
- Best: "[tweet text or summary]" → [numbers if given]
- Why it worked: [your analysis based on hook type, topic, timing]
- Surprise: [what the user mentioned]
- Follower count: [number] (delta: +[N] from last entry)
- Patterns: [1-sentence observation, e.g. "data tweets outperform hot takes 2:1"]
```

If it's the first time (no log exists), create the file and skip the delta.

**Use the log to adjust this week's batch:**
- If data tweets consistently outperform → increase their allocation
- If a topic got strong engagement → suggest doubling down
- If hot takes flopped → reduce contrarian hooks this week
- If a specific posting time worked → note it for the schedule

### Step 1 — Gather context for this week

Ask the user (skip anything already provided):
1. What happened this week worth sharing?
2. Any trends spotted? (or: "find trending topics in [my niche]")
3. Which project is the focus this week?
4. Best tweet from last week to double down on? (already captured in Step 0)

### Step 2 — Allocate the week

Use the **power law split**:

| Type | ~% | What it is | Effort |
|------|----|-----------|--------|
| Quick tweets | 60% | BIP updates, tips, reactions, repurposed | 2-3 min each |
| Engagement | 15% | Questions, polls, hot takes that invite replies | 3-5 min |
| Power bets | 20% | Threads, case studies, data stories | 15-30 min |
| Promo | 5% | Product mentions wrapped in value | 5 min |

Scale to user's schedule. At 3 tweets/day × 6 days = 18 tweets/week:
- ~11 quick, ~3 engagement, ~3 power bets, ~1 promo

### Step 3 — Pick hooks

For each tweet, choose from these formulas:

**Curiosity:** "I was wrong about [belief]." / "[Result] — and it only took [short time]." / "I found [thing] with [big number]. No one's talking about it."

**Story:** "Last week, [unexpected thing] happened." / "3 years ago, I [state]. Today, [state]." / "I almost [big mistake]."

**Value:** "How to [outcome] without [pain]:" / "[Number] things that [outcome]:" / "Stop [mistake]. Do this instead:"

**Contrarian:** "Unpopular opinion: [bold]" / "[Common advice] is wrong. Here's why:" / "I stopped [practice] and [result]."

**Data:** "I analyzed [X] [things]. [Finding]." / "[X]% of [group] make this mistake:"

**Question:** "What's the biggest mistake you see in [field]?" / "Am I the only one who [frustration]?"

**Match hook to type:**
- Quick tweets → Value, Statement
- Engagement → Question, Contrarian
- Power bets → Curiosity, Story, Data
- Promo → Value wrapped around product

### Step 4 — Write tweets

Output each tweet in this format:

```markdown
### [Day] [AM/PM] — [type: quick/engagement/power-bet/promo]

> [Tweet text ready to copy-paste]
>
> [hashtags]

Hook: [which formula] · Pillar: [which pillar] · Project: [which project]
```

For **power bet threads**, also provide:
- Thread structure (hook tweet + 3-7 replies + CTA)
- What visual to include (screenshot, code, data chart)
- Double-down plan: "If this thread does well → [follow-up idea]"

### Step 5 — Append outlier protocol

At the end of every weekly batch, add:

```markdown
## If any tweet this week explodes

Within 4h: Reply to your own tweet with more context
Within 24h: Follow-up thread going deeper
Within 24h: Cross-post to Reddit ([suggest specific subreddits based on focus project])
Within 48h: Pin the follow-up (not the original)
Within 1 week: Turn into blog post or README
Within 1 week: Start a numbered series
```

---

## Output

Save to `tweets/week-YYYY-MM-DD.md` (Monday's date).

If the file already exists, append or ask user if they want to overwrite.

```markdown
# Tweets — Week of [date]
Focus: [project name]
Generated: [timestamp]

## Monday
[tweets]

## Tuesday
[tweets]

...

## Outlier protocol
[reminders with subreddit suggestions]
```

---

## Quality checks (run before delivering)

1. Does the first line of every tweet make you want to read the rest?
2. Is every tweet ≤280 chars? (threads: each tweet ≤280)
3. Does it sound like the user, not like ChatGPT?
4. Are power bets GENUINELY different in quality from quick tweets?
5. Is every product mention wrapped in a story or insight?
6. No two consecutive tweets use the same hook formula?
7. No AI slop: "game-changer", "buckle up", "let that sink in", "unlock", "I'll go first", "masterclass", "deep dive", "paradigm shift"

---

## Performance log (auto-managed)

The file `tweets/log.md` is created and maintained automatically by this skill during Step 0 of every weekly batch. The user never has to edit it manually.

**The skill:**
- Creates the file on first run
- Appends a new entry every Sunday before generating tweets
- Reads past entries to detect patterns and adjust allocation
- Keeps entries for the last 8 weeks (prune older ones)

**What gets logged each week:**
```markdown
# Tweet performance log

## Week of 2026-03-24
- Best: "I analyzed 500 App Store listings..." → ~2400 imp, 89 likes
- Why it worked: Data hook + specific number + contrarian insight
- Surprise: The SwiftUI tip got more saves than expected
- Follower count: 342 (delta: +28)
- Patterns: Data-driven tweets 3x engagement vs opinion tweets
```

**How the log influences generation:**
- 3+ weeks of data → skill auto-adjusts pillar percentages based on what performs
- Identifies the user's "outlier hook type" (the formula that consistently wins)
- Flags when a topic is getting stale (diminishing returns over weeks)
- Suggests new experiments: "You haven't tried a Question hook in 3 weeks — try one this batch"
