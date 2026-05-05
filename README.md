# Claude Skills & Commands

Private backup af mine Claude Code skills og commands.

## Setup på ny computer

```bash
# Klon repo
git clone https://github.com/Fulle4600/claude-skills.git ~/claude-skills-repo

# Kopiér skills
cp -r ~/claude-skills-repo/skills/* ~/.claude/skills/

# Kopiér commands
cp -r ~/claude-skills-repo/commands/* ~/.claude/commands/
```

## Synkroniser ændringer

```bash
cd ~/claude-skills-repo
git pull
cp -r skills/* ~/.claude/skills/
cp -r commands/* ~/.claude/commands/
```

## Push opdateringer fra denne computer

```bash
cd ~/claude-skills-repo
cp -r ~/.claude/skills/* skills/
cp -r ~/.claude/commands/* commands/
git add -A
git commit -m "update skills and commands"
git push
```
