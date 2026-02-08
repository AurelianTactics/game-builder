# Game Builder

Testing using GitHub Actions to trigger Claude. Disabled. Example usage from the output: https://aureliantactics.github.io/game-builder/games/2/
To renable, revert this: https://github.com/AurelianTactics/game-builder/blob/main/.github/workflows/build-game.yml#L11
and create a new API key and add to secrets

## How It Works

1. **Create an Issue** - Use the [game request template](../../issues/new?template=game-request.yml) to describe the game you want
2. **Claude Builds It** - GitHub Actions triggers Claude to build your game
3. **Automatic PR** - A pull request is created with your new game
4. **Play!** - After merge, your game is live on GitHub Pages

## Quick Start

### For Users
Simply [create a new game request](../../issues/new?template=game-request.yml) and describe the game you want!

### For Repository Setup

1. **Clone this repository** or use it as a template

2. **Add your Anthropic API key**:
   - Go to Settings → Secrets and variables → Actions
   - Create a new secret named `ANTHROPIC_API_KEY`
   - Paste your API key from [console.anthropic.com](https://console.anthropic.com)

3. **Enable GitHub Pages**:
   - Go to Settings → Pages
   - Set Source to "Deploy from a branch"
   - Select `main` branch and `/ (root)` folder
   - Save

4. **Enable Auto-merge** (optional but recommended):
   - Go to Settings → General
   - Check "Allow auto-merge"

5. **Update the links**:
   - Edit `index.html` and replace `YOUR_USERNAME` with your GitHub username
   - Update the repository name if different from `game-builder`

## Project Structure

```
game-builder/
├── index.html                          # Landing page with game list
├── games/                              # Generated games folder
│   └── {issue-number}/                 # Each game in its own folder
│       └── index.html                  # Standalone game file
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   └── game-request.yml            # Issue template for game requests
│   └── workflows/
│       └── build-game.yml              # GitHub Actions workflow
└── README.md
```

## Example Games

Once games are built, they'll appear in the `games/` folder. Each game is a standalone HTML file that works offline.

## Configuration

### Workflow Settings

The workflow is configured in `.github/workflows/build-game.yml`. You can adjust:

- `--max-turns 30` - Maximum Claude interactions per game build
- The Claude prompt to change game building instructions
- Branch naming convention

### Trigger Conditions

The workflow runs when:
- An issue is opened or reopened
- The issue has the `game-request` label OR
- The issue title starts with `[Game]`

## Troubleshooting

### Workflow not triggering?
- Check that the issue has the `game-request` label
- Verify `ANTHROPIC_API_KEY` is set in repository secrets
- Check the Actions tab for any errors

### Game not appearing on Pages?
- Wait a few minutes for GitHub Pages to deploy
- Check that the PR was merged successfully
- Verify GitHub Pages is enabled in settings

## License

MIT License - Feel free to use, modify, and distribute.

---

Built with [Claude](https://www.anthropic.com/claude) by Anthropic
