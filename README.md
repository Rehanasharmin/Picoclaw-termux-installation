# Picoclaw Termux Installation Guide (with Telegram Setup)

Picoclaw is a user-friendly, lightweight AI agent. While it offers an Android APK, the app version is functionally limited. The **Termux version**, however, acts as a powerful command-line agent capable of much more. 
This guide walks you through a full installation, fixes the common post-installation errors, and connects it to your Telegram bot using **Ollama's cloud model**.

---

### Step 1: Install Termux
Choose one of the following trusted sources to install Termux:

- **[F-Droid](https://f-droid.org/en/packages/com.termux/)** (Recommended)
- **[Google Play Store](https://play.google.com/store/apps/details?id=com.termux)**

---

### Step 2: Install Dependencies & Pull the AI Model
Open Termux and run the following commands **exactly** as shown. We will update packages, install required tools, and pull the cloud model.

```bash
# Update and upgrade packages
pkg update && pkg upgrade -y

# Install essential packages
pkg install wget python nodejs proot ollama ca-certificates -y

# Pull the cloud model (kimi-k2.5)
ollama pull kimi-k2.5:cloud

# Fix SSL certificate issues for Python/Node
echo "export SSL_CERT_FILE=$PREFIX/etc/tls/cert.pem" >> ~/.bashrc
source ~/.bashrc
```

---

### Step 3: Download and Extract Picoclaw
We will download the latest ARM64 release directly to your Termux home directory.

```bash
# Navigate to your home directory
cd ~

# Download the latest release
wget https://github.com/sipeed/picoclaw/releases/latest/download/picoclaw_Linux_arm64.tar.gz

# Extract the archive
tar xzf picoclaw_Linux_arm64.tar.gz
```

---

### Step 4: Run the Initial Setup & Replace the Config File
First, run the `onboard` command to generate the default configuration folder (`.picoclaw`). Then, replace the default config with a pre-configured one that fixes the common startup bugs.

```bash
# Run onboard to create the default .picoclaw directory
termux-chroot ./picoclaw onboard

# Remove the default config
rm -f ~/.picoclaw/config.json

# Navigate into the .picoclaw folder
cd ~/.picoclaw

# Download the fixed configuration file
wget -O config.json https://raw.githubusercontent.com/Rehanasharmin/Picoclaw-termux-installation/refs/heads/main/config.json
```

---

### Step 5: Configure Your Telegram Bot
Now, we will edit the `config.json` file to add your Telegram Bot Token and your personal Telegram User ID.

Open the file with a text editor:
```bash
nano ~/.picoclaw/config.json
```

**Finding your Bot Token:**
1. Open Telegram and search for **BotFather** (choose the one with the ✅ verified badge).
2. Start a chat and send `/start`.
3. Create a new bot by sending `/newbot` and follow the on-screen instructions to name it.
4. Once created, BotFather will give you an **HTTP API Token** (looks like `1234567890:ABCdefGHIjklMNOpqrSTUvwxYZ`).
5. Copy this token.

**Finding your Telegram User ID:**
1. Go back to Telegram and search for **User Info** (or specifically the bot named **@userinfobot**).
2. Start the bot, and it will instantly reply with your numeric User ID (e.g., `123456789`).
3. Copy this number.

**Editing the JSON file:**
Inside the `config.json` file, scroll down until you find the `"telegram"` block. It will look similar to this:

```json
"telegram": {
    "enabled": true,
    "token": "PASTE YOUR TOKEN HERE",
    "allow_from": [PASTE YOUR ID HERE]
}
```

- Replace `"PASTE YOUR TOKEN HERE"` with your actual Bot Token (keep the quotes).
- Replace `PASTE YOUR ID HERE` with your numeric User ID (do **not** add quotes around the number).

**Save and exit:**
- Press `Ctrl + X` to exit.
- Press `Y` to confirm changes.
- Press `Enter` to save the file.

---

### Step 6: Start the Ollama Server (in a New Session)
Picoclaw relies on Ollama to generate responses. The Ollama server **must run in the background**.
- Swipe from the left edge of the Termux screen to open the **sidebar drawer**.
- Tap on **"New session"** to open a fresh terminal tab.
- In this new tab, run:
```bash
ollama serve
```
> ⚠️ **Keep this tab open and running.** Do not close it while using Picoclaw.

---

### Step 7: Launch the Picoclaw Gateway
Now, return to your **first Termux tab** (where we extracted Picoclaw). Run the gateway command to connect Picoclaw to your Telegram bot:

```bash
cd ~
termux-chroot ./picoclaw gateway
```

---

## ⚠️ IMPORTANT NOTES
- **Always run `ollama serve` in a separate Termux tab** before starting `picoclaw gateway`. If you start the gateway without the server running, your Telegram bot will not reply to your messages.
- You must run `ollama serve` in a new tab **every time** you restart Termux or want to use Picoclaw.

---

## 🎉 Troubleshooting & Final Check
- **Bot doesn't reply?** 
  - Ensure the `ollama serve` tab is still active and hasn't crashed.
  - Double-check your Bot Token and User ID in the `config.json` file—even a single typo will break it.
- **SSL Errors?** 
  - The `export SSL_CERT_FILE` command in Step 2 resolves this. If issues persist, run `source ~/.bashrc` again.

**You're all set!** Send a message to your Telegram bot to test it. Congratulations on completing the setup! 🚀
