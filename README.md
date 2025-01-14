# Disabling the Internal Keyboard on Linux Using `xinput`

This document explains how to disable the internal keyboard of a notebook on Linux systems using the `xinput` command. This procedure is useful in specific scenarios and is compatible with distributions that use the **Xorg** display server.

## When to Use?

This method is helpful for:

- Replacing the internal keyboard with an external keyboard due to physical defects.
- Preventing accidental input (e.g., a broken keyboard typing by itself).
- Temporary configurations for testing or development purposes.

## Prerequisites

- A Linux system based on Xorg.
- Access to the terminal with regular user permissions (or sudo, depending on the system configuration).

## Steps to Disable the Internal Keyboard

### 1. Identify the Keyboard Device

1. Open the terminal.
2. Run the command:
   ```bash
   xinput list
   ```
3. In the output, look for the device representing the internal keyboard. It is usually labeled as **"AT Translated Set 2 keyboard"**.
4. Note down the **ID** associated with the keyboard.

### 2. Disable the Keyboard

1. Use the command below, replacing `<keyboard_ID>` with the noted ID:
   ```bash
   xinput disable <keyboard_ID>
   ```
2. The internal keyboard will be disabled. Test by pressing some keys.

### 3. Re-enable the Keyboard (if needed)

If you want to re-enable the keyboard, use:

```bash
xinput enable <keyboard_ID>
```

## Make the Change Permanent

To automatically disable the keyboard when the system starts:

1. Create a script:
   ```bash
   sudo nano /etc/profile.d/disable_keyboard.sh
   ```
2. Add the following content:
   ```bash
   #!/bin/bash
   xinput disable <keyboard_ID>
   ```
3. Make the script executable:
   ```bash
   sudo chmod +x /etc/profile.d/disable_keyboard.sh
   ```

## Where Does It Work?

### Compatible Systems

- **Ubuntu** and derivatives (Lubuntu, Xubuntu, etc.)
- **Debian**
- **Linux Mint**
- **Fedora** (if configured to use Xorg)
- **Manjaro** and other Arch Linux-based distributions
- **Pop!\_OS**

### Limitations

This method **does not work** on:

- Systems based on the **Wayland** display server.
- Other operating systems, such as **macOS** and **Windows** (which have alternative methods for disabling the keyboard).

## Final Considerations

- This procedure is not permanent unless configured with startup scripts.
- On systems with Wayland, you will need to use other tools or methods.
