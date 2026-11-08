# AGENT.md: Clipping side-income project

Shared context for any AI agent working in this repo. Last updated 2026-11-08.

## Goal
Find out, cheaply and with data, whether short-form video clipping can be a worthwhile side income. If it can, build a pipeline where AI does everything it can reliably do and the human only does what AI cannot: taste, final approval, posting, relationships.

**Do not build the full pipeline until the experiments say it pays** (see "Decision gate").

## Key dates
- **2026-11-10:** GTA 6 preload expected (vendor sources).
- **2026-11-19:** GTA 6 launches on PS5 and Xbox Series X|S. Polymarket put another delay at about 1.9% on 2026-11-08.
- **About 2026-11-29:** decision gate after the experiments.

## What we learned (research, 2026-11-08)
Source quality warning: almost all earnings data comes from companies that sell clipping tools. Treat their numbers as marketing unless independently confirmed.

### How clipping pays
- **Campaign model:** a creator or brand posts a brief with source footage and a rate per 1,000 verified views. Clippers post on their own accounts and submit links. Main marketplaces are Whop Content Rewards (free to join, 7% fee on clipper payouts per the official FAQ) and Vyro, plus direct streamer programs.
- **Advertised rates:** about $0.20 to $6 per 1,000 views, typically about $1. Realized rates are claimed as low as about $0.39 per 1,000 (unsourced vendor figure). One unsourced vendor figure puts the median clipper's lifetime earnings at $24.
- **Math:** $500 a month at $1 per 1,000 views needs about 500k views, roughly 5 to 6 clips a day at 3k views each.
- **Common complaints** (FindClout): rejection after views accrue, bot flags near the payout threshold, budgets depleting before late clips are approved.
- **What separates top earners** (vendor claims): volume (5 to 10 clips a day), picking the moment and hook, and choosing campaigns. Not edit polish.

### What platforms pay directly (third-party estimates, Nov 2026)
| Platform | Per 1,000 views | Catch |
|---|---|---|
| TikTok Creator Rewards | about $0.40 to $1.00 | Videos over 1 minute only; eligibility thresholds |
| YouTube Shorts | about $0.01 to $0.20 | Needs the YouTube Partner Program |
| Facebook Reels | about $0.02 to $0.22 | Content Monetization is invite-only |
| Instagram Reels | none | Brand deals only |
| X | about $0.01 (about $8 to $12 per million verified impressions) | New Original Content Rewards since Aug 2026: Premium, 500 verified followers, 500k verified impressions in 90 days |
| LinkedIn | no general program found | Wrong audience for gaming |

Conclusion: campaigns pay 5 to 100 times more per view than platform programs. Use platforms as places to collect campaign views.

### Rules and risks
- **Rockstar fan-content policy:** calls fan use "non-commercial", but monetized gameplay is tolerated in practice. Takedown categories: leaked or pre-release footage (takedowns active since mid-Aug 2026), isolated cutscenes, endings and spoilers, cheating or exploits, unauthorized mods, and terms-of-service violations. Licensed in-game radio can trigger Content ID claims or Twitch mutes.
- **YouTube:** since Sept 2026, graphic game violence is ad-eligible after the first 7 seconds. The "inauthentic content" policy (clarified July 2026) demonetizes mass-produced or repetitive content and is judged at channel level, so fully hands-off auto-clipping is risky.
- **Permission:** a campaign brief is your licence for its footage. A public VOD is not.
- **FTC:** paid clips are endorsements; disclose as the brief specifies, or ask the campaign owner.
- **Skip:** gambling and crypto campaigns, budgets with under about 3 days of runway, and paid "clipping academies" ($37 to $997; unverified income claims, sometimes no refunds).

### Where the edge is
Generic auto-clippers (OpusClip, Klap, Vizard, Ssemble, Submagic) make clips a commodity. The edge is everything around the cut: choosing the moment, packaging (first 2 seconds, on-screen text, caption), speed, approval rate (following the brief, picking campaigns), distribution (one account per niche, native posting), and not looking mass-produced. The durable moat is the feedback loop of human taste plus your own performance data, not the pipeline code.

## Active campaigns (joined 2026-11-08)
| Campaign | Platforms | Rate per 1,000 | Budget left / total | Cap | Account |
|---|---|---|---|---|---|
| Alliance for Secure AI | TikTok, Instagram, YouTube Shorts | $1.50 | $6,209 / $10,000 | $300 per submission | ai-tech |
| Jo Koy: Blue in the Face | TikTok, Instagram | $2.00 | $17,500 / $17,500 | $500 | comedy |
| Call of Duty: Warzone Season 1 (Clipping Culture) | TikTok $2.00 ($5 minimum), Instagram $1.50 ($4 minimum) | see platforms | about $36.7k / $40,000 | $1,000 | gaming |
| Boxabl (not joined) | TikTok, Instagram, YouTube, X | $0.50 | about $62.3k / $85,000 | $500 | only if testing X |

Campaign URLs are in the conversation history. Full briefs are behind the Content Rewards join wall; record their rules in `campaigns/<name>/rules.json` once pasted.

**Accounts:** use one per niche (gaming, comedy, ai-tech). The gaming account becomes the GTA 6 account, so start it now.

## Experiments (run 2026-11-09 to about 2026-11-29, budget under $50)
Log every clip in `data/clipping-tracker.csv`.

| # | Experiment | When | Pass if |
|---|---|---|---|
| 1 | Market test: 15 to 20 clips across the joined campaigns (week 1: Jo Koy 6, Call of Duty 6, Alliance 5) | Nov 9-15 | Median 1k+ views at 72 hours, 70%+ approved, realized $0.70+ per 1,000 after the fee |
| 2 | Your picks vs the tool: within each campaign, half your picks, half tool auto-picks (`picked_by`) | Nov 9-15 | Your picks get 2x+ the median views |
| 3 | Platform split: same clip on every allowed platform | Ongoing | Shows where to focus |
| 4 | Speed: GTA launch clips posted within 1 hour vs the next day | Nov 19-22 | Fast clips clearly win, which justifies automation |
| 5 | AI hook vs human hook on moments of similar strength | Nov 16-22 | Shows how much packaging to delegate |
| 6 | Unit economics: minutes and dollars per clip, earnings per hour | Ongoing | $15+/hour, or a credible path there |
| 7 | Direct deals: offer 3 free clips to 10 small streamers | Nov 9-22 | 2+ positive replies |

### Decision gate (about Nov 29)
- **Build the pipeline** if experiments 1, 2 and 4 pass. Start with moment-scoring and the review queue.
- **Stop, or pivot to direct streamer retainers,** if experiment 1 fails or experiment 2 shows tools match the human.
- **Keep going solo** if experiment 2 passes but campaigns pay poorly. Build owned accounts and pursue direct deals.

## Pipeline
The plan is in `docs/pipeline-plan.md`. First target: the Call of Duty Warzone S1 campaign, where the source is fixed (trailer plus developer briefing) and the edge is angle variety without near-duplicates.

Build order:
1. **M1:** ingest and index.
2. **M2:** Claude moment mining.
3. **M3:** render 9:16 clips with captions and hook overlay.
4. **M4:** compliance check and tracking.

Stages are swappable adapters so a GTA streamer-VOD adapter can be added by Nov 19.

**Stack:** Python, ffmpeg, faster-whisper, PySceneDetect, Claude API, SQLite. Run locally first; move to the cloud only once volume requires it. YouTube and Twitch often block downloads from datacenter IPs.

**Not automated on purpose:** posting (platform API review, spam-flag risk), Content Rewards submission (no known public API), and view collection at first.

### Open questions blocking M1
1. The locked brief rules for the Call of Duty campaign.
2. The local machine's OS and whether it has a GPU.
3. Whether the human will record voiceovers. Check each brief for AI-voice rules.

## Working rules for agents
- Never commit source videos, renders or credentials. `.gitignore` covers media and `.env`.
- Never post, submit or message anyone on the human's behalf without explicit approval.
- Use only footage covered by a campaign brief. Never use leaked or pre-release GTA footage.
- Label numbers by source quality (official, independent, or vendor claim). Do not present vendor claims as fact.
- Keep per-clip cost (tokens plus compute) to a few cents, and log it.
