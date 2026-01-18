[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Obsidian](obsidian://open?vault=Saarthak's_Headspace&file=Obsidian) > Installation

---
## Flatpack vs Appimage
|Feature|**AppImage** (Recommended for you)|**Flatpak**|
|---|---|---|
|**Philosophy**|"One file, run anywhere." No installation needed.|"Sandboxed application." Isolated from the OS.|
|**Integration**|**Better for System Interaction.** Can easily access system Git, `git-credential-libsecret`, Python, etc.|**Restricted.** Runs in a bubble. Cannot see your system's Git or credentials without complex permissions tweaking reddit+1​.|
|**Updates**|**Self-updating.** Obsidian has a built-in updater that works perfectly inside the AppImage.|**Managed by OS.** You must wait for the Flatpak maintainer to push the update (usually fast, but not instant).|
|**Link Handling**|Requires manual setup or AppImageLauncher to work.|Works out of the box (usually), but breaks if you move the vault.|
For a "power user" workflow (Git, LaTeX, Shell scripts, Python), AppImage is better. Flatpak's sandbox constantly fights against you when trying to use external tools like git or pdflatex

---
#incomplete