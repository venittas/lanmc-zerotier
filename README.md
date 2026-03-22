# lanmc-zerotier
A zero-tier one guide to remote Minecraft LAN connection 

## Pre-requisites
- Java (use openJDK, because open) | [Windows](https://download.java.net/java/GA/jdk26/c3cc523845074aa0af4f5e1e1ed4151d/35/GPL/openjdk-26_windows-x64_bin.zip)

For Windows:
- Download the file linked above
- Extract it to a directory (preferrably inside the User folder)
- Put the `/bin` directory to PATH

To put the `/bin` directory to PATH:
1. Open environment variables (search `environment variables` in Windows Search)
2. Click `Environment variables...`
3. Click Path under `User variables for ___`
4. Click `Browse...` and select the `/bin` directory inside the extracted openJDK

- Minecraft (preferrably, cracked)
- ZeroTier One | [Windows](https://download.zerotier.com/dist/ZeroTier%20One.msi)

To install on Linux:
```zsh
curl -s 'https://raw.githubusercontent.com/zerotier/ZeroTierOne/main/doc/contact%40zerotier.com.gpg' | gpg --import && \
if z=$(curl -s 'https://install.zerotier.com/' | gpg); then echo "$z" | sudo bash; fi
```

> [!IMPORTANT]
> Every player must install and log in to ZeroTier One

## Setup
1. Log in to your Zerotier One account from the app
  - If you haven't already, [create an account](https://central.zerotier.com/).
2. Connect to each other

For Host:
1. Create a network, give it an appropriate name and description (optional)
2. Copy the Network ID and distribute to the members

For Members and Host:

For Windows:

Copy the Network ID and join network through the ZeroTier One taskbar icon (right click and click `Join Network`)

For Linux:
```bash
sudo zerotier-cli join [Network ID]
```

3. Setup Minecraft server (For Host)

Download the official Minecraft server

Terminal for Windows PowerShell:
- If `wget` is not yet installed:
      ```powershell
        Invoke-WebRequest -Uri "https://eternallybored.org/misc/wget/1.21.1/64/wget.exe" -OutFile "C:\Program Files (x86)\GnuWin32\bin\wget.exe"
      ```
  Run this command (creates a MinecraftServer directory inside your User folder and stores the file as `server.jar`:
  ```powershell
    cd ~; mkdir MinecraftServer; cd MinecraftServer; wget https://piston-data.mojang.com/v1/objects/64bb6d763bed0a9f1d632ec347938594144943ed/server.jar -O server.jar
  ```
  GUI:
  1. Download this file (Save Link As...): [Download](https://piston-data.mojang.com/v1/objects/64bb6d763bed0a9f1d632ec347938594144943ed/server.jar)
  2. Create a directory to store the file (optional, whatever works for you)
  3. Save the file inside the directory and rename to `server.jar` (optional, whatever works for you)

After downloading the file, run it with:

```bash
java -Xmx4G -Xms4G -jar server.jar nogui
```

> [!NOTE]
> The `-Xmx4G` and `-Xms4G` are indicators for Java's memory usage; initial heap (memory) and maximum heap (memory) size, respectively
> The command above tells Java to run it with 4gb of RAM
  
After the command finishes, open the `eula.txt` file generated and find the line `eula=false` and change the value to `true`. 
Afterwards, run the command above once again and wait for it to finish. Once finished, open the `server.properties` file and find the line `online-mode=true` and change the value to `false` (for cracked Minecraft support). Next, find the line `server-ip` and put your IP Address from ZeroTier One (the ZT one) as the value. Save the file and run the command once again.
 
4. Join the game

To join the server, both the host and member(s) are to use the IP address of the host from ZeroTier One as the address of the server.
Go to Multiplayer -> Direct Connection -> Paste IP -> Join

5. Enjoy!
