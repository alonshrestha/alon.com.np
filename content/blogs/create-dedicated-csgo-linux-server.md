---
title: 'Ultimate Guide to Set Up CS:GO Dedicated Server Linux'
author: "Alon Shrestha"
pageheading: "Ultimate Guide to Set Up Counter Strike:Global Offensive Dedicated Server in Linux"
date: 2020-11-28
description: "Easy guide to host your dedicated counter-strike: global offensive server on Linux(ubuntu and centos)."
topics: [Linux]
draft: false
cover:
  image: /images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/main.webp
  alt: "Ultimate Guide to Set Up CS:GO Dedicated Server Linux"
  caption: "This post and image originally appeared on my previous website, sTechalon.com"
ShowToc: true
TocOpen: false
---

Do you think playing CS:GO with a ping rate of less than 5 is possible? Think again!

It is definitely possible when you host the game on a personal server. 

With Steam, you can have more control over the game and modify various settings like tick rate, game rules, map pool, plugins, custom skins and many more to make the game more enjoyable.

Want to know how to do this all?

This article covers step-by-step instructions on how to host CS:GO on a dedicated linux server. 

Follow the steps below and host your own cs:go server today!

First step is to choose the server that meets your needs.

For this tutorial, I used the **EC2 t2.micro** server from AWS that has 1 GB RAM, 1 CPU  and 40 GB disk space. This was sufficient for me to play a competitive match with my nine other friends.

However, if you plan to host a server for more players, you may want to opt at least 2GB of RAM or higher.

## CS:GO Server System Requirements
- RAM: 2 GB Minimum - 4 GB Maximum
- CPUs: 2 Minimum
- Disk Space: 40 GB (Recommended)
- Bandwidth: Unlimited (Recommended)
- Operating System: Linux (CentOS, Ubuntu)

Usually, CS:GO can be installed in 15 - 20 GB disk space but due to frequent game updates and space used by OS(Operating System) 40GB disk is recommended for optimal performance.

## Affordable VPS Server For CS:GO
Get an affordable and reliable dedicated hosting server for CS:GO with Hostinger.

![Affordable Hosting For CS:GO Server](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/hostinger.webp)

- RAM: 2 GB
- Disk Space: 40 GB
- Bandwidth: 2 TB
- Price: 5.99/month

&#128073; {{< newtabref  href="https://www.hostg.xyz/SHA2B" title="www.hostinger.com" rel="nofollow">}}

## Setup CS:GO on Linux(Ubuntu/CentOS)

Login to the server with a root user account then install the libraries that support  steamCMD.

*Note: SteamCMD also known as steam console client is a command-line version of steam.*

**Step 1**:  Install the necessary library package.

**For Ubuntu:**
```shell
sudo apt-get install lib32gcc1
```
**For CentOS:**
```shell
yum install glibc.i686 libstdc++.i686
```

**Step 2:** Create a separate user `steam`.
```shell
sudo useradd -m steam
```

**Step 3:** Switch user to `steam`
```shell
su - steam
```

**Step 4:** Create an installation directory.
```shell
mkdir ~/Steam && cd ~/Steam
```

### Download and Install SteamCMD

**Step 5:** Download the latest version of SteamCMD.
```shell
wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz
```

**Step 6**: Extract and run SteamCMD. 
```shell
tar xf steamcmd_linux.tar.gz
./steamcmd.sh
```

After the update is downloaded from Steam, a prompt similar to the image below will appear.
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/1.PNG)

The updated Steam will then provide you with a command prompt as shown in the example below. 

```shell
Steam>
```

**Step 7**: Login to Steam by typing the following command, replacing "userID" and "password" with your own credentials:
```shell
Steam> login <userID> <password>
```
Alternatively, you can log in as an anonymous user by typing:
```shell
Steam> login anonymous
```

**Step 8**: Set the installation directory for CS:GO by typing:
```shell
force_install_dir ./cs_go/
```

**Step 9**: Finally, download and install CS:GO by typing:
```shell
app_update 740 validate
```

This may take some time. Once it's finished, you should see *"Success! App '740' fully installed"* on your screen.

![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/3.PNG)

### Allow TCP and UDP Ports for CS:GO Server Connection
To connect to the game server, make sure that TCP and UDP ports are allowed for all players. The default TCP and UDP port for CSGO server is 27015. 

If your server doesn't allow required TCP and UDP traffic by default, you can find this option in your network settings. 

Alternatively, you can seek help from your hosting provider. Keep in mind that this step is optional if your server firewall is disabled or accepts all network protocols.

![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/4.PNG)

In my case, I have allowed all TCP and UDP ports for everyone.

### Generate a CS:GO Game Auth Token ID
To host a CS:GO game, you need a Steam Auth Token ID. Your Steam account must meet certain requirements to generate the ID. 

You can check the {{< newtabref  href="https://steamcommunity.com/dev/managegameservers" title="requirements" rel="nofollow">}} and get your Auth Token ID by following the steps in the image below.
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/5.PNG)
 
Note: The registered ID for the Counter-Strike: Global Offensive dedicated server is {{< newtabref  href="https://steamdb.info/app/740/" title="appID 740" rel="nofollow">}}, while {{< newtabref  href="https://steamdb.info/app/730/" title="appID 730" rel="nofollow">}} is the official game ID.

After following the steps, you will receive an Auth Token ID that looks similar to **"X38F6E71A3B8G6FE08354AF5BE078"**.

## Run CS:GO on Dedicated Server
To run the CS:GO server, you need to enter a specific command depending on the game mode you want to play. Before running the command, make sure that you are inside the `cs_go` directory. 

Here's an example of the command:

```shell
./srcds_run -game csgo -console -usercon + game_type 0 + game_mode 0 + mapgroup mg_active + map de_dust2 + sv_setsteamaccount "YOUR AUTH TOKEN" THISGSLTHERE -net_port_try
```

For different modes, you need to  change the game_mode value.

**Casual** = game_mode 0

**Competitive** = game_mode 1 

**Deathmatch** = game_mode 2 

Remember to replace "YOUR AUTH TOKEN" with your own authentication token.

Once you've entered the command, you'll see the public IP of your game server.
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/7.PNG)

## Join CS:GO Server

To join a CS:GO server, you can use either of the following methods:

**Method 1:** Connect through the game console.

- Launch CS:GO and enable the developer console in the game settings.
![Downloading and Installing SteamCMD In Linux | sTechalon.com](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/8.webp)

- Return to the dashboard and open the console using the `~` key.

- Type in `connect <your-ip-address>` to join the server.
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/9.png)

**Method 2:** Add the server IP to your favourites list

- Launch CS:GO and go to the Community Server Browser.
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/10.webp)

- Click on the Favourites tab.
- Add your server IP to the list and connect to it.
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/12.png)

## Run CS:GO In Background

If you log out from the server, your game will be disconnected or stopped, and you can't host the game logged in 24x7. 

However, you can host the game in a background session, and the game will continue to run even if you log out from the server. To do this, you need to install the screen application on your server.

To install screen on Ubuntu, run the following command:
```shell
sudo apt-get install screen -y
```

To install screen on CentOS, run the following command:
```console
sudo yum install screen -y
```
After installation, create a new session named "csgo" by typing the following command:
```shell
screen -R csgo
```
Now run the game host command. In this example, we are running the competitive game mode:

```shell
./srcds_run -game csgo -console -usercon + game_type 0 + game_mode 1 + mapgroup mg_active + map de_dust2 + sv_setsteamaccount  “YOUR AUTH TOKEN” THISGSLTHERE -net_port_try
```

When the game is hosted successfully, you can detach the screen session by pressing the following keys at the same time:
`Crtl + a + d`

Now you are out of that session. To see the running background session, type:
```shell
screen -ls
```

You will see output like this:
```console
There is a screen on:
    7166.csgo    (Detached)
1 Socket in /run/screen/S-stechalon.
```

In the above output, **7166** is the ID, and **csgo** is the name of the screen. To rejoin the detached screen, type: 
```shell
screen -r 7166
```

## Secure your CS:GO Server with a Hostname and Password

To add a layer of security to your CS:GO server, you can configure a hostname and password. This will ensure that only authorized players can join the game.

First, locate the autoexec.cfg file and open it. Add your desired hostname and password to the file.

To set the hostname, add the following line: hostname "your_hostname_here"

To set the password, add the following line: password "your_password_here"
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/13.PNG)

Save the file and exit.

Next, refresh your favourite list and check the hostname. You should now see the changes you made reflected there.
![Downloading and Installing SteamCMD In Linux](/images/posts/how-to-create-your-own-csgo-counter-strike-global-offensive-dedicated-custom-server-ubuntu-centos/14.png)

If you want to customize your CS:GO game further, {{< newtabref  href="https://developer.valvesoftware.com/wiki/Counter-Strike:_Global_Offensive_Dedicated_Servers" title="CS:GO advanced configuration" rel="nofollow">}} article can be a helpful resource.

## Change CS:GO Tick Rate

Tick rate refers to the frequency at which the game server updates the game state and sends the information to players. 

The higher the tick rate, the more frequently the server updates the game state, resulting in a more accurate representation of player actions and movements.

To change the tick rate in CS:GO, you need to add some commands to the autoexec.cfg file located in `csgo/cfg/autoexec.cfg`. 

Add the following lines to the file:
- sv_minupdaterate 128
- sv_mincmdrate 128

This simple step will improve your game performance and make your gameplay experience smoother. For more information on tick rates, you can refer to this {{< newtabref  href="https://win.gg/news/4379/explaining-tick-rates-in-fps-games-difference-between-64-and-128-tick" title="article" rel="nofollow">}}.

## Update Your CS:GO Dedicated Server
Regular updates are released for CS:GO every week or month, and to keep your server running smoothly, it's important to update it as well. 

To update your CS:GO game on your dedicated server, you need to follow the **steps 6 to 9** which involve from running SteamCMD to app update. These steps will guide you through the process of updating your game.

## How to Achieve Low Ping in CS:GO Gameplay
Achieving low ping in CS:GO gameplay is crucial for a smooth and enjoyable gaming experience. Here are some tips to help you reduce your ping:
- **Host the game near your region:** Choose a server that is located near your region to reduce the ping. The closer the server is to your location, the lower the ping will be.
- **Use a well-known hosting provider:** Choose a reputable hosting provider that offers reliable and fast servers. A well-maintained server with a stable network connection can help you achieve low ping.
- **Use a VPN:** A VPN can help you reduce your ping by selecting a server location that is closer to the game server. 
However, be sure to choose a VPN that offers fast and stable connections.
By implementing these tips, you can significantly reduce your ping and enjoy a lag-free CS:GO gameplay experience.

## Wrapping Up - How to Host a CS:GO Dedicated Server

Congratulations! You have successfully set up your own CS:GO server on a personal dedicated server. In this guide, we covered everything you need to know to get started with hosting a CS:GO server, from installing and configuring the server to updating it and optimizing gameplay.

If you have any questions or concerns, please don't hesitate to leave a comment below. 

Thanks for reading and happy gaming!