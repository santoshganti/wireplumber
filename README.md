# WirePlumber Configuration for SteamOS & Linux Gaming

## 🎮 Purpose of This Repository

This repository provides **WirePlumber configuration files** designed to enhance **audio behavior on SteamOS, Bazzite, and other Linux gaming distros**. The goal is to **fix common audio issues, prevent unwanted device switching, and improve compatibility**—all without requiring root access. These configurations are **stored in `~/.config/wireplumber/`**, ensuring they **persist across OS updates** while remaining easy to modify or remove.

### ✅ What This Repo Fixes / Improves:

- **Fixes DualSense haptic feedback issues** by renaming its PipeWire audio sink to match what games expect.
  
  - Some games rely on a specific sink name for haptics to work correctly.
  - This is implemented in `wireplumber.conf.d` to ensure compatibility with newer versions of WirePlumber.
  - **Reference:** [Reddit - DualSense Haptic Feedback Issue][reddit-dualsense]

- **Prevents PlayStation controllers from hijacking audio output** (e.g., DualSense becoming the default device).

- **Keeps Bluetooth headsets in high-quality A2DP mode** instead of auto-switching to low-quality HFP.

- **Stops HDMI and Bluetooth audio from suspending**, reducing audio delays after idle periods.

- **Improves audio behavior in virtual machines (VMs)** by increasing buffer sizes.

- **Disables ******\`\`****** on gaming devices** where it's not needed (e.g., Steam Deck/Bazzite setups).

- **Disables ******\`\`****** seat monitoring for Bluetooth**, preventing multi-user conflicts that can cause unintended audio device switching. This is especially useful for gaming setups where multiple user sessions or Steam's `gamescope-session` might interfere with Bluetooth audio behavior.

### 🆚 What’s Different From SteamOS / Bazzite?

This project **builds on existing SteamOS & Bazzite configurations** but improves upon them by:

- **Making everything user-configurable** inside `~/.config/wireplumber/` so updates won't wipe changes.
- **Organizing files better** (proper numbering to ensure correct load order).
- **Adding compatibility fixes** from the **Arch Wiki & community findings**.
- **Providing legacy support for WirePlumber versions that still rely on Lua scripts**.
- **Giving users an easy way to undo changes** if they want to revert.

### 🔄 Why Lua Scripts Are Included

Some devices and older Linux distributions still depend on the **legacy WirePlumber Lua configuration format**. While WirePlumber now recommends using **SPA-JSON configuration files**, Lua scripts are available in this repository for users running outdated versions or specific devices that still require them.

- If you are using **WirePlumber 0.5+**, migrating to SPA-JSON is recommended for better compatibility and future support.
- Lua scripts remain available in this repository for systems that have not yet transitioned to the newer configuration format.

For more details, see the **[WirePlumber migration guide](https://pipewire.pages.freedesktop.org/wireplumber/daemon/configuration/migration.html)**. If you need legacy Lua scripts, they can be found in the `legacy/` folder of this repository. To use them, copy the scripts into your WirePlumber configuration directory:

```bash
cp -r legacy/main.lua.d ~/.config/wireplumber/
```

Then restart WirePlumber:

```bash
systemctl --user restart wireplumber
```

---

## 🛠️ How to Install

1. **Backup your existing WirePlumber configs** (so you can restore later if needed):
   ```bash
   mv ~/.config/wireplumber ~/.config/wireplumber-bak
   ```
2. **Clone this repository and copy the files into your WirePlumber config folder:**
   ```bash
   git clone https://github.com/YOUR_GITHUB_USERNAME/wireplumber-configs.git
   cp -r wireplumber-configs/wireplumber.conf.d ~/.config/wireplumber/
   ```
3. **Restart WirePlumber to apply the changes:**
   ```bash
   systemctl --user restart wireplumber
   ```

---

## 🔄 How to Undo Changes

If you experience issues or want to **restore your previous settings**:

1. **Remove the custom configurations:**
   ```bash
   rm -rf ~/.config/wireplumber/wireplumber.conf.d
   ```
2. **Restore your original WirePlumber configs (if you made a backup earlier):**
   ```bash
   rm -rf ~/.config/wireplumber && mv ~/.config/wireplumber-bak ~/.config/wireplumber
   ```
3. **Restart WirePlumber:**
   ```bash
   systemctl --user restart wireplumber
   ```

---

## 📚 References

- Some configurations are adapted from **SteamOS & Bazzite's WirePlumber policies**.
- Additional fixes & improvements are based on information from the **Arch Wiki** and other Linux audio troubleshooting resources.
- See official documentation for further customization:
  - [WirePlumber Documentation](https://pipewire.pages.freedesktop.org/wireplumber/)
  - [Arch Linux Wiki - PipeWire](https://wiki.archlinux.org/title/PipeWire)
  - [WirePlumber Migration Guide](https://pipewire.pages.freedesktop.org/wireplumber/daemon/configuration/migration.html)
  - [Reddit - DualSense Haptic Feedback Issue](https://www.reddit.com/r/linux_gaming/comments/190dypz/dualsense_haptic_feedback_wont_work_for_me/?utm_source=chatgpt.com)

---

## ⚠️ Disclaimer

These scripts **should not harm your device**, but **use them at your own risk**.

**This is a hobby project** made publicly available **to help others facing similar issues**. The author **is not responsible** for any unintended effects, but **feedback & contributions are welcome!** 🚀

