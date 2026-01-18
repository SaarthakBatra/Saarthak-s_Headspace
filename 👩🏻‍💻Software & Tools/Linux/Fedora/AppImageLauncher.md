[📁 Explore](obsidian://open?vault=Saarthak's_Headspace&file=📁%20Explore) > [Linux](obsidian://open?vault=Saarthak's_Headspace&file=Linux) > [Fedora](obsidian://open?vault=Saarthak's_Headspace&file=Fedora) > AppImageLauncher

---
## Installation Guide for Fedora
1.  **Open the Release Page:**
    Go to this URL in your web browser:
    [https://github.com/TheAssassin/AppImageLauncher/releases](https://github.com/TheAssassin/AppImageLauncher/releases)

2.  **Find the Latest Release:**
    *   Look for the entry at the top marked **"Latest"** (usually version `v2.2.0` or similar).
    *   Scroll down to the **"Assets"** section of that release.
    *   *Note: You may need to click "Show all assets" if the list is collapsed.*

3.  **Download the Correct RPM:**
    Find the file ending in `.rpm` that matches your architecture (usually `x86_64` for standard Intel/AMD laptops).
    *   **Look for:** `appimagelauncher-X.X.X-travisXXX.XXX.x86_64.rpm`
    *   **Do NOT download:** The ones ending in `.deb` (for Ubuntu) or `i386` (for old 32-bit PCs).
    *   Click the file to download it to your **Downloads** folder.

4.  **Install via Terminal (Final Step):**
    Once downloaded, you need one simple command to install it. Open your terminal and run:

    ```bash
    sudo dnf install ~/Downloads/appimagelauncher*.rpm
    ```
    *(The `*` is a wildcard, so you don't have to type the long confusing numbers in the filename).*

5.  **Verify & Use:**
    *   Now, double-click your Obsidian AppImage.
    *   You should see the "Integrate and Run" popup.
    *   Once integrated, your `obsidian://` links will work correctly (after you update the Vault ID/Name as discussed).

6. Fix the Desktop Entry
	AppImageLauncher created a `.desktop` file for you, but we need to edit it to handle URLs correctly.

	1.  Open your terminal.
	2.  Find the desktop file. It is located in `~/.local/share/applications/`.
		```bash
		ls ~/.local/share/applications/appimagekit_*.desktop
		```
	    *(You will see a file with a long name like `appimagekit_hash_Obsidian.desktop`)*.
	3.  Edit that file:
		```bash
		nano ~/.local/share/applications/appimagekit_YOUR_FILE_NAME.desktop
		```
	4.  Find the line starting with `Exec=`. It probably looks like this:
		```ini
		Exec=/home/username/Applications/Obsidian.AppImage
		```
	5.  **Append ` %U` to the end of that line.** It must look like this (note the space before `%U`), remove any other tags like --no-sandbox:
		```ini
		Exec=/home/username/Applications/Obsidian.AppImage %U
		```
	6.  Save (`Ctrl+O`, `Enter`) and Exit (`Ctrl+X`).
7. Update the Database
Tell the system to reload the desktop configuration:
```bash
update-desktop-database ~/.local/share/applications/
```


### Resources

1. RPM Packages - https://github.com/TheAssassin/AppImageLauncher/releases
2. Project Github - https://github.com/TheAssassin/AppImageLauncher

---
#incomplete