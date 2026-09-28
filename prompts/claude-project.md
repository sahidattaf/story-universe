# Claude Project
# STORY UNIVERSE — Claude Project (FFOAO)

## GOAL
Build and publish Sahid J. Attaf's 12-chapter image book and ongoing video content engine.

## COORDINATOR AGENT (Main Thread)
- Scopes work: "Write Chapter 7" → breaks into tasks
- Delegates: assigns to specialized threads
- Reviews: checks output against style guide
- Assembles: merges chapter + images + video script

## THREADS

### THREAD 1: NARRATIVE WRITER
- Reads: character-profile.md, visual-style-guide.md
- Outputs: 600-800 word chapter narrative
- Tests: Bilingual summary + palette consistency

### THREAD 2: IMAGE PROMPT GENERATOR
- Reads: chapter narrative, visual-style-guide.md
- Outputs: 5 Midjourney/DALL-E prompts per chapter
- Tests: Camera angle + lighting + mood for each

### THREAD 3: VIDEO SCRIPT CONVERTER
- Reads: chapter narrative, content-engine/scripts/
- Outputs: 7-12 min video script (long) + 3-5 min (short)
- Tests: Hook + B-roll + CTA

### THREAD 4: NOTION SYNC AGENT
- Tools: GitHub read, Notion API write
- Outputs: Push chapters, scripts, images to Notion
- Schedule: Daily cron at 06:00 Curaçao time

### THREAD 5: ANALYTICS AGENT
- Tools: YouTube API, TikTok API
- Outputs: Weekly performance report
- Schedule: Friday cron at 08:00

### THREAD 6: MONETIZATION AGENT
- Tools: Affiliate tracker, Sponsorship pipeline
- Outputs: Revenue dashboard
- Schedule: Monthly cron