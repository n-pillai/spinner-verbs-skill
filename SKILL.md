---
name: spinner-verbs
description: "Create personalized Claude Code spinner verbs for users based on their life, interests, and personality. Use this skill whenever someone asks to customize their Claude Code spinner, personalize their spinner verbs, make custom spinnerVerbs, or mentions wanting to change the text that appears while Claude Code is thinking. Also trigger when users mention Daniel Miessler's spinner verbs post, PAI spinner customization, or say things like 'make my terminal more fun' or 'personalize my Claude Code experience.'"
---

# Spinner Verbs Personalizer

## Overview

Claude Code displays rotating "spinner verbs" while it's working (e.g., "Thinking...", "Processing..."). These can be customized in `~/.claude/settings.json`. This skill guides users through creating a deeply personalized set of spinner verbs drawn from their own life — their profession, hobbies, favorite books/movies/music, cultural background, inside jokes, and personal philosophy.

The goal is not generic fun verbs. It's verbs that make the user smile because they recognize something true about themselves every time one scrolls by.

## How Spinner Verbs Work

The configuration lives in `~/.claude/settings.json`:

```json
{
  "spinnerVerbs": {
    "mode": "append",
    "verbs": [
      "Your-verb-here",
      "Another-verb-here"
    ]
  }
}
```

- **`"mode": "append"`** — Adds user's verbs to the built-in defaults (recommended starting point)
- **`"mode": "replace"`** — Only shows the user's verbs, no defaults
- All verbs should be present participles (ending in "-ing")
- Keep verbs short enough to render cleanly in a terminal line
- Hyphenate multi-word verbs (e.g., `Rubber-duck-debugging`)
- Aim for 100+ verbs to avoid frequent repeats; 300-500+ for a "rarely see the same one twice" experience

## The Interview Process

The quality of spinner verbs depends entirely on how well you know the person. Don't guess — ask. The process is conversational and iterative: draft categories, show the user, let them approve/cut/redirect.

### Step 1: Seed Categories

Start by asking the user about the major areas of their life. Present these as a starting framework, not a final list:

**Always ask about:**
- What they do for work (job title, industry, daily tools, jargon)
- Hobbies and interests outside work
- Favorite books, movies, TV shows, music
- Cultural background and heritage
- Whether they cook, travel, play sports, play games
- Personal philosophy or mindset frameworks they connect with
- Family life (kids, pets — these generate great verbs)
- Side projects or creative pursuits

**Ask about preference:**
- Mode: append (mix with defaults) or replace (only their verbs)?
- Target count: ~50 (tight), ~150 (good variety), ~300+ (rarely repeats)?
- Anything that should NOT appear (too personal, too exposing, work-sensitive)?

### Step 2: Draft by Category

Generate verbs in batches organized by category. Present each category to the user with:
1. The category name
2. Where you pulled the inspiration from (be transparent)
3. The full list of proposed verbs
4. A few callouts of ones you think are particularly good and why

**Wait for the user's feedback on each category before moving on.** They may want to:
- Keep the whole category
- Cut specific verbs
- Cut the entire category
- Add things you missed
- Redirect the category entirely

This is the most important part of the process. Resist the urge to dump all categories at once.

### Step 3: Go Deeper on What Matters

Pay attention to which categories get enthusiastic responses vs. lukewarm ones. Double down on what lights the user up. If they love the cooking verbs, ask about specific cuisines and techniques. If they have strong opinions about books, ask for their actual reading list — don't guess from the zeitgeist.

**Common pitfalls to avoid:**
- **Generic tech-bro picks**: Books like "Zero to One", "Atomic Habits", "Deep Work" are fine if the user actually loves them, but don't assume. Ask.
- **Hokey cultural references**: If adding verbs from someone's cultural heritage, cast a wide net but flag that you're guessing and invite correction. Heritage is personal — don't assume which traditions resonate.
- **Too-personal or risky verbs**: Some categories (career transitions, financial details, health) might be things the user doesn't want in a config file that others could see. Ask before including sensitive areas.
- **Project-specific verbs**: Some users want verbs about their projects; others find it too narrow or time-bound. Ask.
- **Self-help flattery**: Avoid verbs that sound like affirmations or motivational posters. The best verbs are specific, wry, and real — not aspirational.

### Step 4: Check for Gaps

After going through all categories, review what's missing. Common areas people forget:
- Travel and exploration
- Reading habits (not just what they read, but the act of reading)
- Social activities (book clubs, trivia nights, game nights)
- Seasonal or holiday traditions
- Pet-related verbs
- Local/regional life (city-specific humor)
- The meta experience of using Claude Code itself

### Step 5: Generate the Final File

Produce a clean, valid JSON file with:
- No comments (JSON doesn't support them)
- No duplicates
- Proper formatting
- A total verb count reported to the user

Validate the JSON programmatically before delivering it.

## Deployment Instructions

Include these with every delivered file:

### Installation

1. **Check for existing settings:**
   ```bash
   cat ~/.claude/settings.json
   ```

2. **If the file doesn't exist:**
   ```bash
   mkdir -p ~/.claude
   cp [downloaded-file] ~/.claude/settings.json
   ```

3. **If settings already exist**, merge the `spinnerVerbs` block into the existing JSON alongside other settings. Don't overwrite the whole file.

4. **Restart Claude Code** — quit the current session and start a new one.

5. **Verify** — ask Claude Code to do something and watch for your custom verbs in the spinner.

### Known Issues

There is an open bug (GitHub issue #23347) where `spinnerVerbs` in user-level `~/.claude/settings.json` can sometimes be ignored. If verbs don't appear:
- Try placing them in a project-level settings file: `.claude/settings.json` within your project directory
- If using `append` mode and it's not working, try `replace` mode

### Maintenance

- Add new verbs anytime by editing `~/.claude/settings.json`
- No restart needed after editing — changes take effect on next spinner cycle
- Keep a backup of your verbs file; it represents real curation effort

## Quality Checklist

Before delivering the final file, verify:
- [ ] All verbs end in "-ing" (present participle form)
- [ ] Multi-word verbs are hyphenated
- [ ] No duplicates
- [ ] Valid JSON (parse it programmatically)
- [ ] Verb count reported to user
- [ ] User has approved or reviewed every category
- [ ] Nothing too personal/risky included without explicit approval
- [ ] Deployment instructions provided

## Example Categories

These are examples only — every user's categories will be different. The best spinner verbs come from asking, not assuming.

| Source | Example Verbs |
|--------|---------------|
| Software engineering | `Yak-shaving`, `Rubber-duck-debugging`, `Bikeshedding` |
| Cooking | `Mise-en-place-ing`, `Maillard-reacting`, `Deglazing` |
| Literature (Pratchett) | `Vimes-booting`, `Granny-Weatherwax-headologying`, `Ook-ing` |
| Literature (Wodehouse) | `Jeeves-shimmering`, `Aunt-Agatha-avoiding` |
| Parenting | `Screen-time-negotiating`, `Lunchbox-packing` |
| Indian cooking | `Tadka-sizzling`, `Mustard-seed-popping`, `Kerala-parotta-layering` |
| British TV | `Fawlty-Towering`, `Humphrey-Appleby-obfuscating` |
| Philosophy | `Kintsugi-repairing`, `Sisyphus-imagining-happy` |
| Travel | `Passport-stamping`, `Guidebook-ignoring` |
| Trivia | `Useless-knowledge-deploying`, `Category-sweeping` |
