# Picoclaw termux installation guid with telegram setup.
We are familiar with Picoclaw, noting that it is user-friendly and lightweight. Although it has its own Android APK, its functionality is somewhat limited within the app. However, Picoclaw's Termux version acts as a versatile agent capable of performing a wide range of tasks. Please be aware that there are some issues associated with Picoclaw, particularly after installation.But this **setup Guid** fixes it. **This setup guide will assist you in using Ollama effectively.**

# Step 1.
install termux from [F droid](https://f-droid.org/en/packages/com.termux/) Or [Play store](https://play.google.com/store/apps/details?id=com.termux)

# Step 2.
```Shell
pkg update & upgrade
pkg install wget python nodejs proot
# Download the latest release
wget https://github.com/sipeed/picoclaw/releases/latest/download/picoclaw_Linux_arm64.tar.gz
tar xzf picoclaw_Linux_arm64.tar.gz
termux-chroot ./picoclaw onboard   # chroot provides a standard Linux filesystem layout
```
