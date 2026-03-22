# 🐦 Weekly Tweet Engine

**Batch-generate a week of strategic tweets in ~15 minutes.** Power-law-optimized content for indie devs building in public.

A single-file Claude Code / Cursor / Codex skill that turns your Sunday planning session into a full week of ready-to-post tweets — with automatic performance tracking that gets smarter over time.

---

## The problem

You know you should tweet. You know build-in-public works. But every day you stare at the compose box thinking "what do I even post?"

So you either don't post, or you post something generic that gets 3 likes.

## The solution

One skill file. One command on Sunday. 18 tweets for the week.

The skill uses **power law content theory** (80% volume tweets + 20% high-effort "power bets") combined with **proven hook formulas** from marketing research to generate tweets that are strategically allocated across your week.

It also tracks your performance over time and auto-adjusts — if your data tweets consistently outperform your hot takes, next week's batch shifts accordingly.

---

## Quick start

### 1. Install (30 seconds)

```bash
# Claude Code
mkdir -p .claude/skills/weekly-tweet-engine
cp SKILL.md .claude/skills/weekly-tweet-engine/SKILL.md

# Cursor / Codex
mkdir -p .agents/skills/weekly-tweet-engine
cp SKILL.md .agents/skills/weekly-tweet-engine/SKILL.md
```

### 2. First run — setup your profile

Paste this into Claude Code or Cursor:

```
Read the skill at .claude/skills/weekly-tweet-engine/SKILL.md.
Then ask me a few questions to create my tweet profile at tweets/profile.md.
Keep it short — just my projects, voice, and schedule.
```

The skill asks ~8 questions and creates a 40-line profile. Takes 2 minutes.

### 3. Generate your weekly batch

Every Sunday, paste this:

```
Read tweets/profile.md and the skill at .claude/skills/weekly-tweet-engine/SKILL.md.
Run the weekly review first (ask me about last week's performance).
Then generate my tweets for this week:

- This week I [what happened]
- Trends I spotted: [any trends, or "none, find some"]
- Focus project: [which project gets the power bets]
```

**Output:** A `tweets/week-YYYY-MM-DD.md` file with your entire week of tweets, organized by day, tagged by type and hook formula.

---

## What it generates

### Tweet types (power law split)

| Type | ~% | What it is |
|------|----|-----------|
| Quick tweets | 60% | BIP updates, tips, reactions — your "lottery tickets" |
| Engagement | 15% | Questions, polls, hot takes that drive replies |
| Power bets | 20% | Threads, case studies, data stories — your outlier candidates |
| Promo | 5% | Product mentions always wrapped in value |

### Each tweet includes

```markdown
### Wednesday AM — power-bet (thread)

> The "10 Game" is going viral on TikTok right now.
> 2 players count 1-10, replacing numbers with words each round.
> There's no app for it.
> So I'm building one this weekend.
> Here's the concept 🧵
>
> #buildinpublic #indiedev

Hook: Curiosity + Story · Pillar: Viral trends · Project: 1$forYourNewApp
```

For power bet threads: full thread structure + visual suggestions + double-down plan if it performs.

---

## Hook formulas included

The skill has 7 hook families built in:

| Hook | Best for | Example opener |
|------|----------|----------------|
| **Curiosity** | Power bets, threads | "I found a niche with 2M searches and 3 apps..." |
| **Story** | BIP updates, threads | "Last Tuesday I spotted a trend at 11pm..." |
| **Value** | Quick tweets, educational | "How to get 1,000 downloads without ads:" |
| **Contrarian** | Engagement, hot takes | "Unpopular opinion: 6 months on your app is wrong" |
| **Data** | Power bets, credibility | "I analyzed 500 App Store listings..." |
| **Question** | Engagement drivers | "Do you spend more time on code or metadata?" |
| **Statement** | Quick tweets, punchy | "Your subtitle is your most underrated asset." |

Plus a **banned words list** to avoid AI slop: "game-changer", "buckle up", "let that sink in", "unlock", "masterclass", etc.

---

## Auto-managed performance tracking

The skill creates and maintains `tweets/log.md` automatically.

**Every Sunday before generating new tweets, it asks you 4 quick questions:**

1. Best tweet this week? (paste or describe)
2. Rough numbers? (impressions/likes, or "did well"/"flopped")
3. Follower count now?
4. Anything that surprised you?

It logs the answers, analyzes patterns, and uses them to adjust next week's batch:

- 3+ weeks of data → auto-adjusts pillar percentages
- Identifies your winning hook type
- Flags stale topics
- Suggests experiments ("You haven't tried a Question hook in 3 weeks")

You never edit `log.md` manually. It maintains itself.

---

## Outlier protocol

When a tweet performs unusually well, the skill includes a ready-made escalation plan:

```
Within 4h  → Reply with additional context
Within 24h → Follow-up thread going deeper
Within 24h → Cross-post to Reddit (skill suggests specific subreddits)
Within 48h → Pin the follow-up
Within 1 week → Turn into blog post / README / product feature
Within 1 week → Start a numbered series
```

Trigger it anytime with:
```
My tweet about [topic] got [X impressions]. Run the outlier protocol.
```

---

## File structure

After a few weeks of use, your project looks like this:

```
tweets/
├── profile.md              ← your voice, projects, schedule (auto-created)
├── log.md                  ← performance tracking (auto-managed)
├── week-2026-03-24.md      ← batch for this week
├── week-2026-03-31.md      ← batch for next week
└── ...
```

One skill file in `.claude/skills/`. Everything else is generated.

---

## Other commands

### Mid-week quick generation
```
Read tweets/profile.md. Write 3 tweets about [topic/trend/milestone].
Use the hook formulas from the tweet engine skill.
```

### After a viral tweet
```
Read tweets/profile.md. My tweet about [topic] got [X impressions / Y likes].
Run the outlier protocol: generate follow-up thread + Reddit cross-post + series plan.
```

### Update your profile (when you pivot)
```
Read tweets/profile.md. I'm now focusing on [new project] instead of [old project].
Update my profile and adjust the content pillars.
```

---

## Works great with

- **[coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)** — The `social-content` and `copywriting` skills complement this one. This skill handles the generation pipeline; those handle platform strategy and copy polish.
- **[rgranet/designlint](https://github.com/rgranet/designlint)** — If you're tweeting about shipping UI, DesignLint makes sure it doesn't look like AI slop before you screenshot it.

---

## The theory behind it

This skill is built on two frameworks:

**Power law content strategy** — In content, 1% of posts generate ~85% of total reach. You can't predict which tweet will be the outlier, so you need volume (lottery tickets) + quality (power bets) to let the math work. The 80/20 split is calibrated for this.

**Corey Haines' social-content framework** — Hook formulas, content pillars, engagement routines, and repurposing workflows adapted from the [marketingskills](https://github.com/coreyhaines31/marketingskills) repo.

The combination: you post enough to buy lottery tickets, but each ticket is optimized with proven hooks and backed by your personal performance data.

---

## Compatibility

| Agent | Status |
|-------|--------|
| Claude Code | ✅ Tested |
| Cursor | ✅ Compatible |
| Codex | ✅ Compatible |
| Gemini CLI | 🔄 Should work (untested) |

---

## Contributing

Found a hook formula that works? A better way to structure the weekly review? PRs welcome.

---

## License

MIT

---

Built by [Ruben Granet](https://x.com/rubengranet) · Part of the [1$forYourNewApp](https://1foryournewapp.com) ecosystem
