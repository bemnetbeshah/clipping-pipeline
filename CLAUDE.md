# CLAUDE.md

@AGENT.md

## Claude-specific notes
- `AGENT.md` holds the shared project context, findings, experiments and decision gate, and is imported above. Update it there, not here, so other agents see the same state.
- For fresh trend research (what clippers are saying now, new campaigns, platform rule changes), use the `last30days` skill (github.com/mvanhorn/last30days-skill). In cloud sandboxes its Reddit search is often blocked and it has no X, TikTok or YouTube coverage without `yt-dlp` and a ScrapeCreators key, so add host web search.
- Before writing Claude API code, check current model IDs and pricing rather than relying on memory. Use a cheaper model for bulk moment mining and a stronger one for the final hook pass.
- When the human pastes experiment data, compute each experiment's pass or fail against the thresholds in `AGENT.md` and update the "Decision gate" status.
