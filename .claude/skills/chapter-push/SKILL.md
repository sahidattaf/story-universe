---
name: chapter-push
description: Push a Story Universe chapter from the local repo to Notion. Use when the user says "push Chapter N", "sync Chapter N", or "send Chapter N to Notion".
---

# chapter-push

Push a Story Universe chapter from the local markdown file to the Notion "📋 Story Universe — Chapters" database.

## When to use this skill

Trigger when the user says any of:
- "push Chapter N"
- "sync Chapter N"
- "send Chapter N to Notion"
- "chapter N to Notion"

## Prerequisites

The chapter markdown file must exist at:
`story-bible/chapters/{NN}-{slug}.md`

where `{NN}` is the zero-padded chapter number (01, 02, ..., 17) and `{slug}` is the kebab-case title.

If the file doesn't exist, STOP and tell the user to create it first.

## Notion targets

- **Database:** 📋 Story Universe — Chapters
- **Data source ID:** `5b36090e-7e9e-40c2-a178-9c7b246200f9`
- **Command Center page ID:** `3e9a269fc94780f58178c3c674ec4c88`

## Workflow

1. **Read the local file.** Parse the markdown from `story-bible/chapters/{NN}-{slug}.md`.

2. **Verify the file structure.** The file must contain:
   - A narrative section (prose paragraphs)
   - A "Five Image Prompts" section with 5 numbered prompts
   - A "Video Script — Long Form" section
   - A "Video Script — Short Form" section
   - A "Papiamentu Summary" section

   If any section is missing, STOP and report which one.

3. **Query the Chapters database** for an existing row where Chapter Number = N.
   - Use `notion-query-data-sources` on `5b36090e-7e9e-40c2-a178-9c7b246200f9`.
   - Filter by `Chapter Number equals N`.

4. **Decide CREATE vs UPDATE:**
   - If a row exists → UPDATE that page (properties + body).
   - If no row exists → CREATE a new page.

5. **Populate properties:**
   - Title: `Chapter {N}: {Title}`
   - Chapter Number: `{N}`
   - Status: `Draft`
   - Word Count: auto-computed with `wc -w` on the full file
   - Validation Passed: true
   - Palette Used: comma-separated from the chapter
   - GitHub Path: `story-bible/chapters/{NN}-{slug}.md`

6. **Add body blocks in this exact order:**
   - Heading 1: chapter title
   - Paragraphs: narrative (one paragraph per block)
   - Heading 2: "Five Image Prompts"
   - Numbered list: 5 prompts
   - Heading 2: "Video Script — Long Form"
   - Paragraphs: script segments
   - Heading 2: "Video Script — Short Form"
   - Paragraphs: script segments
   - Heading 2: "Papiamentu Summary"
   - Paragraphs: summary

7. **Return:**
   - The page URL
   - Confirmation of whether it was CREATE or UPDATE
   - A summary table: Title | Chapter Number | Status | Word Count

## Rules

- **Never paraphrase.** Use the text exactly as it appears in the local file.
- **Never create duplicates.** Always check for an existing row first.
- **Bilingual is required.** If the Papiamentu summary is missing, STOP.
- **Palette must be consistent.** Reference the visual style guide if unclear.

## Example

User: "push Chapter 18"

You:
1. Read `story-bible/chapters/18-....md`
2. Verify structure
3. Query Chapters DB for Chapter Number = 18
4. Update or create
5. Return URL and summary table