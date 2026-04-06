# Picoclaw termux installation guid with telegram setup.
We are familiar with Picoclaw, noting that it is user-friendly and lightweight. Although it has its own Android APK, its functionality is somewhat limited within the app. However, Picoclaw's Termux version acts as a versatile agent capable of performing a wide range of tasks. Please be aware that there are some issues associated with Picoclaw, particularly after installation.But this **setup Guid** fixes it. **This setup guide will assist you in using Ollama effectively.**

# Step 1.
install termux from [F droid](https://f-droid.org/en/packages/com.termux/) Or [Play store](https://play.google.com/store/apps/details?id=com.termux)

# Step 2.
```Shell
pkg update && pkg upgrade -y
pkg install wget python nodejs proot ollama -y

ollama pull kimi-k2.5:cloud

pkg install ca-certificates

echo "export SSL_CERT_FILE=$PREFIX/etc/tls/cert.pem" >> ~/.bashrc
source ~/.bashrc

# Download the latest release
wget https://github.com/sipeed/picoclaw/releases/latest/download/picoclaw_Linux_arm64.tar.gz

# Extract the archive
tar xzf picoclaw_Linux_arm64.tar.gz

# Run the application using termux-chroot
termux-chroot ./picoclaw onboard
```
# Step 3

After the **installation** run:
```Shell
rm .picoclaw/config.json
cd .picoclaw
wget -O config.json https://raw.githubusercontent.com/Rehanasharmin/Picoclaw-termux-installation/refs/heads/main/config.json
```

# Step 4
```Shell
nano config.json
```
Or(if you aren't in .picoclaw directory)
```Shell
nano .picoclaw/config.json
```

Go to **Telegram** and search **Botfather** click on the one that has **verified** badge. then click **start**, Name your bot and after it will give you a token, copy that and paste into "PASTE YOUR TOKEN HERE" in the config.jsons telegram channels block. then goto **telegram** for second time and search **User info** click on the "User info ° get ID ° idbot°" one and click start it will show your ID copy the ID and paste in to "allow_from": [Paste Your ID Here], in the telegram block.

# Step 5

Create new tab in termux and run/Click on the "new session" button from the termux's sidebar and run:
```Shell
ollama serve
```

# Step 6

Go back to previous tab and run:
```Shell
termux-chroot ./picoclaw gateway
```

# IMPORTANT ⚠️
if you start gate way and send massage to telegram and doesn't get models reply then You forget to make new tab in termux and forget to run 
```Shell
ollama serve
```
YOU SHOULD RUN THIS COMMAND IN NEW TAB EVERYTIME YOU RUN PICOCLAW!

# THANKS 👍 
THANKS FOR FOLLOWING IT

