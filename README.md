# 🌍 Adding Ukrainian & Russian Keyboard Layouts to Arch Linux (i3wm) ⌨️

A simple guide to set up Ukrainian (ua) and Russian (ru) keyboard layouts alongside English (us) in Arch Linux with i3 window manager.

## ⚡ Quick Method (Temporary)

Add this to your i3 config file (`~/.config/i3/config`):

```bash
exec --no-startup-id setxkbmap -layout us,ua,ru -variant ,winkeys, -option grp:alt_shift_toggle
```

🔑 **What this does:**
- Sets English (us) as primary layout
- Adds Ukrainian (ua) with winkeys variant
- Adds Russian (ru) with default variant
- Uses `Alt+Shift` to toggle between layouts

## 🔄 Permanent Methods

### Method 1: Xorg Configuration
1. Create config file:
   ```bash
   sudo nano /etc/X11/xorg.conf.d/00-keyboard.conf
   ```
2. Add:
   ```ini
   Section "InputClass"
       Identifier "system-keyboard"
       MatchIsKeyboard "on"
       Option "XkbLayout" "us,ua,ru"
       Option "XkbVariant" ",winkeys,"
       Option "XkbOptions" "grp:alt_shift_toggle"
   EndSection
   ```

### Method 2: Using localectl
```bash
sudo localectl set-x11-keymap us,ua,ru ,winkeys, grp:alt_shift_toggle
```

## 🖥️ Show Layout in i3 Status Bar
Add to `~/.config/i3status/config`:
```ini
order += "keyboard_layout"

keyboard_layout {
    format = " ⌨ %s"
}
```

## 🔍 Verification
Check current layout with:
```bash
setxkbmap -query
```

## 💡 Tips
- Use `setxkbmap -layout ua` to temporarily switch to Ukrainian
- The `winkeys` variant matches Windows keyboard layout
- Change `alt_shift` to `ctrl_shift` if preferred

## 🚀 Reload Configurations
After changes:
1. Restart i3: `Mod+Shift+R`
2. Or logout/login

---

📌 **Note:** For TTY console (non-Xorg), configure separately using `loadkeys` or `localectl`.
