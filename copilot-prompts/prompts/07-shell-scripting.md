# Shell Scripting Prompts

This section provides prompts for generating and improving shell scripts using GitHub Copilot.

## Bash Scripting

### Automate File Backup

**Use Case:** Creating a Bash script to back up a directory.

**The Prompt:**
```bash
# Write a Bash script to back up a directory to a specified location
# - Accept source and destination as arguments
# - Compress the backup
# - Log the operation
```

**Example Output:**
```bash
#!/bin/bash

SRC_DIR="$1"
DEST_DIR="$2"
LOG_FILE="backup.log"

if [ -z "$SRC_DIR" ] || [ -z "$DEST_DIR" ]; then
  echo "Usage: $0 <source_dir> <destination_dir>"
  exit 1
fi

TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
BACKUP_FILE="$DEST_DIR/backup_$TIMESTAMP.tar.gz"

tar -czf "$BACKUP_FILE" -C "$SRC_DIR" .

if [ $? -eq 0 ]; then
  echo "[$(date)] Backup successful: $BACKUP_FILE" >> "$LOG_FILE"
else
  echo "[$(date)] Backup failed" >> "$LOG_FILE"
fi
```

**Explanation:** This prompt is effective because it specifies the script's requirements, including argument handling, compression, and logging, guiding Copilot to generate a robust backup script.

## Zsh Scripting

### Custom Zsh Prompt

**Use Case:** Creating a custom Zsh prompt that shows Git branch and exit status.

**The Prompt:**
```zsh
# Write a Zsh prompt (PS1) that shows:
# - Current directory
# - Git branch (if in a git repo)
# - Last command exit status (with color)
```

**Example Output:**
```zsh
autoload -Uz vcs_info
precmd() { vcs_info }

setopt prompt_subst

PS1='%F{cyan}%~%f$(git_prompt_info)%(?..%F{red}✗%f%? )%# '

git_prompt_info() {
  if [ -d .git ] || git rev-parse --git-dir > /dev/null 2>&1; then
    echo " (%F{yellow}$(git rev-parse --abbrev-ref HEAD 2>/dev/null)%f)"
  fi
}
```

**Explanation:** This prompt is effective because it specifies the desired features for the Zsh prompt, guiding Copilot to generate a prompt that displays the current directory, Git branch, and exit status with color coding.
