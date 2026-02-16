# Spinner Verbs Skill for Claude Code

A Claude Code skill that helps you create deeply personalized spinner verbs drawn from your own life — your profession, hobbies, favorite books/movies/music, cultural background, inside jokes, and personal philosophy.

## What Are Spinner Verbs?

Claude Code displays rotating "spinner verbs" while it's working (e.g., "Thinking...", "Processing..."). These can be customized in your `~/.claude/settings.json` file to show personalized messages that make you smile every time one scrolls by.

Instead of generic messages, imagine seeing:
- `Tadka-sizzling` (if you love Indian cooking)
- `GNU-Terry-Pratchetting` (if you're a Discworld fan)
- `Rubber-duck-debugging` (if you're a developer)
- `Sunday-pancake-making` (if that's your family tradition)

## Installation

### 1. Install the Skill

```bash
# Create the skills directory if it doesn't exist
mkdir -p ~/.claude/skills/spinner-verbs

# Download the skill file
curl -o ~/.claude/skills/spinner-verbs/SKILL.md https://raw.githubusercontent.com/n-pillai/spinner-verbs-skill/main/SKILL.md
```

**Windows (PowerShell):**
```powershell
# Create the skills directory if it doesn't exist
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills\spinner-verbs"

# Download the skill file
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/n-pillai/spinner-verbs-skill/main/SKILL.md" -OutFile "$env:USERPROFILE\.claude\skills\spinner-verbs\SKILL.md"
```

### 2. Use the Skill

Once installed, you can invoke it in Claude Code:

```bash
/spinner-verbs
```

Or just ask Claude Code to help you personalize your spinner verbs, and it will automatically use this skill.

The skill will guide you through an interactive interview process to create spinner verbs based on:
- Your profession and work life
- Hobbies and interests
- Favorite books, movies, TV shows, music
- Cultural background and heritage
- Family life and traditions
- Personal philosophy and mindset frameworks
- And much more!

## Example Verbs

See `example-verbs.json` for a real-world example with 533+ verbs covering:
- Federal Reserve & finance terminology
- AI/ML engineering concepts
- Indian culture and Kerala traditions
- Cooking techniques (French, Indian, general)
- Literature (Pratchett, Wodehouse, Le Guin, Tolkien, and more)
- Classic films and British comedy
- Parenting and family life
- Bay Area culture
- Philosophy (Stoicism, Buddhism, Japanese concepts)
- Software engineering
- Travel and exploration
- Book club culture
- And many more categories!

## Quick Start (Using Example Verbs)

If you want to use the example verbs as a starting point:

```bash
# Download the example verbs
curl -o ~/nisha-spinner-verbs.json https://raw.githubusercontent.com/n-pillai/spinner-verbs-skill/main/example-verbs.json

# Merge with your existing settings.json or create new one
```

Then edit your `~/.claude/settings.json` to include the spinnerVerbs configuration from the example file.

## How It Works

The skill follows a conversational, iterative process:

1. **Seed Categories**: Asks about major areas of your life
2. **Draft by Category**: Generates verbs in batches, showing you each category for approval
3. **Go Deeper**: Doubles down on categories you're enthusiastic about
4. **Check for Gaps**: Reviews what might be missing
5. **Generate Final File**: Produces a clean, valid JSON file ready to use

The skill emphasizes asking rather than guessing, ensuring your verbs are authentic and personal to you.

## Configuration Format

Spinner verbs are configured in `~/.claude/settings.json`:

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

- **`"mode": "append"`** — Adds your verbs to the built-in defaults (recommended)
- **`"mode": "replace"`** — Only shows your verbs, no defaults
- All verbs should be present participles (ending in "-ing")
- Hyphenate multi-word verbs (e.g., `Rubber-duck-debugging`)
- Aim for 100+ verbs to avoid repeats; 300-500+ for variety

## Troubleshooting

### Verbs Not Appearing

There's a known issue (GitHub issue #23347) where `spinnerVerbs` in `~/.claude/settings.json` can sometimes be ignored. If your verbs don't appear:

1. Try placing them in a project-level settings file: `.claude/settings.json` within your project directory
2. If using `append` mode doesn't work, try `replace` mode
3. Restart Claude Code after making changes

## Contributing

Found a bug or have a suggestion? Please open an issue or submit a pull request!

## Credits

Created by Nisha Pillai ([@n-pillai](https://github.com/n-pillai))

Inspired by the Claude Code community's love for personalization and the idea that the best developer tools feel like they were made just for you.

## License

MIT License - feel free to use, modify, and share!
