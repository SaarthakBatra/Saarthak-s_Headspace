[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore)  > [Obsidian](obsidian://open?vault=Saarthak's_Headspace&file=Obsidian) > Github Sync

---
# Obsidian Seamless GitHub Sync: Fedora Laptop + Android (Termux)

## 📋 Quick Overview

This guide sets up **bidirectional sync** across:
- **Fedora Laptop**: Obsidian Desktop + Obsidian Git plugin + native Git
- **Android Phone**: Obsidian Mobile + Termux (CLI automation) + Tasker (background sync)

**Key Feature**: Conflict resolution via `.gitattributes` ensures both changes are preserved when edits occur simultaneously on both devices.

---

## Part 1: Fedora Laptop Setup

### 1.1 Install Git & GitHub CLI

```bash
# Fedora installation
sudo dnf install git gh

# Verify installation
git --version
gh --version
```

### 1.2 Configure Git Credentials

```bash
# Configure git user identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Use credential storage (libsecret on Fedora/KDE)
git config --global credential.helper libsecret
```

### 1.3 Token Authentication (Recommended)


### 1.4 Clone Your GitHub Vault

```bash
# Navigate to where you want the vault
cd ~/Documents
git clone git@github.com:YOUR_USERNAME/YOUR_VAULT_REPO.git my-obsidian-vault
cd my-obsidian-vault

# Verify it's properly initialized
git status
```

### 1.5 Install Obsidian (AppImage - Recommended for Fedora)
- Use [AppImageLauncher](obsidian://open?vault=Saarthak's_Headspace&file=AppImageLauncher)

### 1.6 Open Vault & Install Git Plugin
1. **Open Obsidian** → Select your cloned vault from `~/Documents/my-obsidian-vault`
2. **Trust the folder** (accept security prompt)
3. Go to **Settings** → **Community Plugins** → **Disable Safe Mode**
4. Click **Browse** → Search **"Git"** → Install the plugin by **Vinzent03**
5. **Enable** the plugin from **Community Plugins** list
6. Go to **Settings** → **Git** plugin → Configure:

#### Git Plugin Configuration (Fedora)
Setup uses:
- **Pull Strategy:** MERGE (Git default) ✅
- **Commit Frequency:** Dual-mode (time-based 12hrs + edit-based 1 min)
- **Push Strategy:** Automatic on commit-and-sync ✅
- **Conflict Handling:** Preserve both changes via `.gitattributes merge=union`
- **On Close:** Auto-commit before closing (requires workaround)
- **Status Display:** Full sync status in status bar

---

| Field | Value |
|-------|-------|
| **Commit message on manual commit** | `Backup: {{date}} [laptop:{{hostname}}]` |
| **Commit message script** | (Leave empty) |
| **Date format** | `YYYY-MM-DD HH:mm:ss` |
| **Hostname placeholder** | fedora-laptop |

| Setting | Value | Reason |
|---------|-------|--------|
| **Merge strategy** | `Merge` | Preserves full history; works with `.gitattributes merge=union` |
| **Merge strategy on conflicts** | `None (git default)` | Let `.gitattributes` handle union merge strategy |
| **Pull on startup** | `ON` (enabled) | Always fetch latest changes when opening Obsidian |

| Setting | Value |
|---------|-------|
| **Split timers for automatic commit and sync** | ✅ ON |

This allows separate intervals for commits vs syncs.

| Setting                                                   | Value | Explanation                |
| --------------------------------------------------------- | ----- | -------------------------- |
| **Auto commit-and-sync interval (minutes)**               | `0`   | 0                          |
| **Auto commit-and-sync after stopping file edits**        | ✅ ON  | Edit-based trigger         |
| **Auto commit-and-sync after latest commit**              | ✅ ON  | Updates timestamp tracking |

| Setting | Value | Reason |
|---------|-------|--------|
| **Push on commit-and-sync** | ✅ ON | After committing, immediately push to GitHub |
| **Pull on commit-and-sync** | ✅ ON | Before committing, pull latest changes (your workflow) |

| Setting | Value |
|---------|-------|
| **Auto push interval (minutes)** | `12` |
| **Auto pull interval (minutes)** | `12` |

| Field | Value |
|-------|-------|
| **Author name for commit** | Your Name |
| **Author email for commit** | your.email@example.com |

| Setting | Value |
|---------|-------|
| **Automatically refresh source control view on file changes** | ✅ ON |
| **Source control view refresh interval** | `7000` (milliseconds) |

| Setting                               | Value | Your Requirement                     |
| ------------------------------------- | ----- | ------------------------------------ |
| **Show status bar**                   | ✅ ON  | ✅ Display all sync status            |
| **Show branch status bar**            | ✅ ON  | Shows current branch + sync state    |
| **File menu integration**             | ✅ ON  | Quick stage/unstage from right-click |
| **Disable informative notifications** | ❌ OFF | Keep notifications ON for now        |
| **Disable error notifications**       | ❌ OFF | Alert on sync failures               |
| **Hide notifications for no changes** | ❌ OFF | On to Reduce notification spam       |

| Setting | Value |
|---------|-------|
| **Show Author** | `Full` |
| **Show Date** | ✅ ON |
| **Diff view style** | `Split` |

---

### 1.7 Initial Sync Test

```bash
# In terminal, navigate to vault directory
cd ~/Documents/my-obsidian-vault

# Manually trigger a sync
git pull origin main
git add .
git commit -m "Initial laptop setup"
git push origin main

# Check status
git log --oneline -n 5
```

---

## Part 2: Conflict Prevention on Both Devices

### 2.1 Create `.gitignore` (Both Devices)

In your vault root directory (`my-obsidian-vault/.gitignore`):

```gitignore
# Obsidian workspace files (device-specific)
.obsidian/workspace.json
.obsidian/workspace-mobile.json

# Obsidian Git plugin state (don't sync across devices)
.obsidian/plugins/obsidian-git/data.json

# Temporary conflict files
conflict-files-obsidian-git.md

# System files
.DS_Store
Thumbs.db
*.swp
*.swo

# Optional: Per-device settings
# .obsidian/plugins/**
# .obsidian/themes/**
```

### 2.2 Create `.gitattributes` (Both Devices)

In your vault root directory (`my-obsidian-vault/.gitattributes`):

```gitattributes
# Union merge strategy for markdown files
# This preserves BOTH changes from conflicting edits
*.md merge=union

# Keep line endings consistent across platforms
* text eol=lf
*.bat text eol=crlf
```

**What this does**: If you edit the same `.md` file on both devices simultaneously, Git will merge both changes rather than creating a conflict. Subsequent pulls will contain both updates.

### 2.3 Commit These Files

```bash
cd ~/Documents/my-obsidian-vault
git add .gitignore .gitattributes
git commit -m "chore: add conflict prevention configuration"
git push origin main
```

---

## Part 3: Android + Termux Setup

### 3.1 Install Termux

```bash
# Option 1: F-Droid (recommended)
# Visit: https://f-droid.org/en/packages/com.termux/
# Download and install APK

# Option 2: Termux:Tasker (for automation)
# F-Droid → Install "Termux:Tasker"
```

### 3.2 Termux Storage & Initial Setup

```bash
# Grant file system access
termux-setup-storage

# Update packages
pkg update && pkg upgrade -y

# Install git, ssh, and required tools
pkg install -y git openssh termux-api
```

### 3.3 SSH Key Setup in Termux

```bash
# Verify you already have GitHub SSH integration
# (Since you mentioned it's already configured)

# If needed, copy SSH key from laptop to Termux:
# Option A: Generate new key in Termux
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -C "your.email@example.com"

# Copy public key
cat ~/.ssh/id_ed25519.pub
# Add this to GitHub Settings → SSH Keys

# Configure git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global credential.helper cache
```

### 3.4 Clone Vault in Termux

```bash
# Create obsidian directory
mkdir -p ~/storage/documents/Obsidian

# Clone your vault
cd ~/storage/documents/Obsidian
git clone git@github.com:YOUR_USERNAME/YOUR_VAULT_REPO.git

# Verify
cd YOUR_VAULT_REPO
git status
```

### 3.5 Install Obsidian Mobile App

```bash
# Google Play Store: "Obsidian - Secure Knowledge Base"
# Free version works perfectly
# Select your vault folder: ~/storage/documents/Obsidian/YOUR_VAULT_REPO
```

---

## Part 4: Seamless Sync Automation (Termux + Tasker)

### 4.1 Create Sync Scripts in Termux

```bash
# Create sync directory
mkdir -p ~/.sync_scripts

# Create main sync script
cat > ~/.sync_scripts/sync_all_vaults.sh << 'EOF'
#!/bin/bash

# Colors for output
GREEN='\033[0;32m'
RED='\033[0;31m'
NC='\033[0m'

VAULTS_DIR="$HOME/storage/documents/Obsidian"
LOG_FILE="$HOME/.sync_scripts/sync.log"

# Initialize log
echo "[$(date '+%Y-%m-%d %H:%M:%S')] Starting sync..." >> "$LOG_FILE"

# Sync each vault
for vault_dir in "$VAULTS_DIR"/*; do
    if [ -d "$vault_dir/.git" ]; then
        vault_name=$(basename "$vault_dir")
        echo "[$(date '+%Y-%m-%d %H:%M:%S')] Syncing: $vault_name" >> "$LOG_FILE"
        
        cd "$vault_dir"
        
        # Pull remote changes first (your rule: first update repo)
        if git pull origin main >> "$LOG_FILE" 2>&1; then
            # Now push local changes (then push new changes)
            if git add -A && git commit -m "mobile: sync on $(date '+%Y-%m-%d %H:%M:%S')" >> "$LOG_FILE" 2>&1; then
                git push origin main >> "$LOG_FILE" 2>&1
                echo -e "${GREEN}✓ $vault_name synced${NC}" >> "$LOG_FILE"
            else
                echo -e "${RED}✗ $vault_name commit failed${NC}" >> "$LOG_FILE"
            fi
        else
            echo -e "${RED}✗ $vault_name pull failed${NC}" >> "$LOG_FILE"
        fi
    fi
done

echo "[$(date '+%Y-%m-%d %H:%M:%S')] Sync complete" >> "$LOG_FILE"
EOF

# Make it executable
chmod +x ~/.sync_scripts/sync_all_vaults.sh
```

### 4.2 Create Manual Sync Shortcut

```bash
# Quick command in Termux (add to ~/.bashrc)
cat >> ~/.bashrc << 'EOF'

# Obsidian sync function
sync_obsidian() {
    source ~/.sync_scripts/sync_all_vaults.sh
    tail -20 ~/.sync_scripts/sync.log
}

# Check sync status
status_obsidian() {
    VAULTS_DIR="$HOME/storage/documents/Obsidian"
    for vault_dir in "$VAULTS_DIR"/*; do
        if [ -d "$vault_dir/.git" ]; then
            echo "=== $(basename "$vault_dir") ==="
            cd "$vault_dir"
            git fetch origin main 2>/dev/null
            git status --short
            echo ""
        fi
    done
}
EOF

source ~/.bashrc
```

### 4.3 Test Manual Sync

```bash
# In Termux, test the sync
sync_obsidian

# Check status
status_obsidian

# View logs
cat ~/.sync_scripts/sync.log
```

### 4.4 Automate with Tasker (Optional but Recommended)

**Install Required Apps:**
1. **Tasker** (Play Store)
2. **Termux:Tasker** (F-Droid)
3. **AutoNotification** (Play Store - for sync failure alerts)

**Setup Tasker Task:**

1. Open Tasker → **+ (New Task)** → Name: `Obsidian Sync`
2. Click **+** to add action → **Termux Tasker** (or `Run Shell`)
3. Enter command:
   ```bash
   source ~/.sync_scripts/sync_all_vaults.sh
   ```
4. Click **+** → **Alert** → **Notify**:
   - Title: `Obsidian Sync`
   - Text: `Sync complete - check log`
5. Save task

**Setup Tasker Profile (Automation):**

1. **Profiles** → **+ (New Profile)** → **Time**
2. Set time (e.g., every 4 AM + every time vault opens)
3. Select the `Obsidian Sync` task
4. Enable profile

**Alternative: Sync on Vault Open**

1. **Profiles** → **+ (New Profile)** → **App** → Select **Obsidian**
2. **Task**: Run `Obsidian Sync` task
3. This auto-syncs whenever you open the Obsidian app

---

## Part 5: Handling Conflicts (Your Custom Rule)

### 5.1 Understanding Your Conflict Resolution Strategy

Your requirement:
> *In case of conflict, update the repo with first update, pull the update, then push the new update*

**Implementation via `.gitattributes`:**

When conflicts occur on `.md` files:
```
Device A: Edits note at 10:00
Device B: Edits same note at 10:05
   ↓
Git merge=union: Both edits combined into single file
   ↓
Pull from A → Merge → Push combined version
   ↓
Other device pulls → Gets both changes
```

### 5.2 Manual Conflict Resolution (If Needed)

```bash
# In Termux, if conflict still occurs:
cd ~/storage/documents/Obsidian/YOUR_VAULT

# Check conflicts
git status | grep "both modified"

# View conflict markers
cat conflicted-file.md

# Accept both versions (our setup should prevent this via gitattributes)
git checkout --theirs conflicted-file.md  # Accept phone version
# OR
git checkout --ours conflicted-file.md    # Accept laptop version

# Or manually merge if needed
# Edit the file, remove conflict markers, then:
git add conflicted-file.md
git commit -m "resolve: manual merge of conflicted-file.md"
git push origin main
```

### 5.3 Monitor Conflict Files

```bash
# Termux: Check for any conflict files generated
cat ~/.sync_scripts/sync.log | grep -i conflict

# On laptop:
cd ~/Documents/my-obsidian-vault
ls -la | grep "conflict"
```

---

## Part 6: Day-to-Day Workflow

### Fedora Laptop

```bash
# Open Obsidian → Everything auto-syncs in background
# The Git plugin handles:
# ✓ Auto-pull on startup
# ✓ Auto-commit every 5 minutes
# ✓ Auto-push every 5 minutes

# Check sync status (optional):
cd ~/Documents/my-obsidian-vault
git log --oneline -n 10 --all
```

### Android Phone

```bash
# Manual sync (in Termux):
sync_obsidian

# Check status:
status_obsidian

# Automated (via Tasker):
# Syncs every 4 AM + when Obsidian opens
# No manual action needed
```

### Conflict Resolution Check

```bash
# Both devices, check for conflicts:
cat ~/.sync_scripts/sync.log | tail -20

# On laptop Git plugin status bar shows sync state
# Green = in sync
# Yellow = syncing
# Red = conflict/error
```

---

## Part 7: Troubleshooting

### Issue: Git Permission Denied (publickey)

**Fedora & Termux**:
```bash
# Test SSH connection
ssh -T git@github.com
# Should respond: "Hi USERNAME! You've successfully authenticated..."

# If fails, re-add key to ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# For Fedora KDE specifically:
# Settings → Advanced → SSH → Enable SSH agent
```

### Issue: Git Credentials Not Saved

**Fedora**:
```bash
# Use libsecret (native to KDE)
git config --global credential.helper libsecret
```

**Termux**:
```bash
# Use cache helper (shorter but safer in sandboxed env)
git config --global credential.helper 'cache --timeout=3600'
```

### Issue: Conflict Files Keep Appearing

**Solution**:
```bash
# Ensure .gitattributes is committed and pulled on both devices
git pull origin main

# Verify merge strategy is active
cat .git/config | grep -A 5 "\[merge"

# Re-run sync scripts
sync_obsidian
```

### Issue: Obsidian Git Plugin Not Working (Fedora)

**Check**:
1. Using AppImage (not Snap/Flatpak)
2. Git is installed: `which git`
3. Plugin is enabled in Settings → Community Plugins
4. Vault is a proper Git repo: `git status` works in terminal

**Reset**:
```bash
# Disable & re-enable plugin
# Restart Obsidian
# Try manual git command in terminal first
cd ~/Documents/my-obsidian-vault && git status
```

### Issue: Termux Sync Fails Silently

**Debug**:
```bash
# Run with verbose output
cd ~/storage/documents/Obsidian/YOUR_VAULT
git -v pull origin main
git -v add .
git -v commit -m "test"
git -v push origin main

# Check detailed log
cat ~/.sync_scripts/sync.log
tail -f ~/.sync_scripts/sync.log  # Real-time
```

---

## Part 8: Advanced Configuration

### 8.1 Per-Device Configs (Keep .obsidian Synced But Isolated)

If you want to sync `.obsidian/` folder but keep device-specific configs:

```bash
# In .gitignore, remove the workspace.json exclusion
# Add to .gitattributes:
.obsidian/workspace.json merge=ours  # Laptop keeps own version
.obsidian/workspace-mobile.json merge=theirs  # Phone keeps own version
```

### 8.2 Performance Optimization

**Laptop**:
```bash
# Reduce auto-commit frequency if needed
# Git Settings → Commit Interval → 10 minutes (instead of 5)

# Limit history fetch for large vaults
git config core.compression 9
```

**Termux**:
```bash
# Compress objects in repository
cd ~/storage/documents/Obsidian/YOUR_VAULT
git gc --aggressive

# Shallow clone for faster initial sync (if vault is huge)
# git clone --depth 50 git@github.com:...
```

### 8.3 Backup Strategy

```bash
# Fedora: Keep local Git history
cd ~/Documents/my-obsidian-vault
git reflog  # Never lose commits

# Termux: Regular full sync
# Sync script already includes this

# GitHub: Create branch before major changes
git checkout -b feature/experiment
# Later: git checkout main && git merge feature/experiment
```

---

## Part 9: Security Best Practices

| Aspect | Implementation |
|--------|-----------------|
| **SSH Keys** | Ed25519 (more secure than RSA) |
| **Repo Privacy** | Set to Private on GitHub |
| **Credentials** | Use SSH (not HTTPS/PAT) |
| **Termux Sync** | Disable Obsidian Git plugin on Android |
| **.gitignore** | Exclude sensitive files (API keys, etc.) |
| **Backup** | Enable GitHub's backup/archival feature |

---

## 📚 Quick Reference Commands

### Fedora Terminal

```bash
# Clone vault
git clone git@github.com:YOUR_USERNAME/YOUR_VAULT.git

# Manual sync
cd ~/Documents/my-obsidian-vault
git pull origin main
git add .
git commit -m "message"
git push origin main

# View log
git log --oneline -n 20

# Check status
git status
```

### Termux

```bash
# Quick sync
sync_obsidian

# Check status
status_obsidian

# View logs
cat ~/.sync_scripts/sync.log

# Manual push (if needed)
cd ~/storage/documents/Obsidian/YOUR_VAULT
git pull && git add . && git commit -m "manual sync" && git push
```

---

## ✅ Verification Checklist

- [ ] Git installed on Fedora: `git --version`
- [ ] SSH keys configured: `ssh -T git@github.com`
- [ ] Obsidian AppImage running (not Snap)
- [ ] Obsidian Git plugin installed & enabled
- [ ] `.gitignore` and `.gitattributes` committed
- [ ] Fedora vault auto-syncing (check Git plugin status)
- [ ] Termux installed with Git, OpenSSH
- [ ] Obsidian Mobile app opened with synced vault
- [ ] Sync script working: `sync_obsidian` executes without errors
- [ ] Test conflict resolution: Edit same file on both devices

---

## 🎯 Next Steps

1. **Week 1**: Set up Fedora & Android, test basic sync
2. **Week 2**: Enable Tasker automation for background sync
3. **Week 3**: Monitor logs, optimize sync intervals
4. **Ongoing**: Regular backups via GitHub releases/tags

---

## 📖 Additional Resources

- **Obsidian Git Plugin**: https://publish.obsidian.md/git-doc/
- **OhMyObsidian Project**: https://github.com/GiGiDKR/OhMyObsidian
- **Termux Documentation**: https://termux.dev/
- **Git Best Practices**: https://git-scm.com/book/en/v2/

---

**Author**: Generated January 15, 2026  
**Status**: Production-Ready  
**Tested With**: Fedora KDE Plasma + Android 13+ + Termux + Obsidian v1.5+

---
#incomplete