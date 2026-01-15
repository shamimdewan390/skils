# install claude with copilot

```bash
brew install --cask claude-code
```
```bash
claude --version
```

```bash
code ~/.claude/settings.json
```

## paste below code in  ```~/.claude/settings.json```
```javacript
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://localhost:4141",
    "ANTHROPIC_AUTH_TOKEN": "test",
    "ANTHROPIC_MODEL": "claude-sonnet-4.5",
    "ANTHROPIC_SMALL_FAST_MODEL": "gpt-4.1"
  }
}
```


## It should be run in one terminal

```bash
 npx copilot-api@latest start
```


> jodi install na hoe tahobe
```
 ls -al
```
then remove 2 files ```.claude.json ``` and ```.claude.json.backup ```
or
```bash
 rm -rf .claude.json.backup
 rm -rf .claude.json
```

```bash
claude
```
> Authenticate: On first run, it will open your browser to log in with your Claude.ai account (you need a Claude Pro or Max subscription)



Ghostty
