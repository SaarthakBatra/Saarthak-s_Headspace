[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Linux](obsidian://open?vault=Saarthak's_Headspace&file=Linux) > Fedora

---
## Community Repositories
1. [[COPR]]
## Tools
1. [[AppImageLauncher]]

## Commands
#### Session Type (Wayland or X11)
```bash
echo "$XDG_SESSION_TYPE"
```
```bash
loginctl show-session "$(loginctl | awk '$1 ~ /^[0-9]+$/ {print $1; exit}')" -p Type -p Desktop -p Remote
```

---
#incomplete