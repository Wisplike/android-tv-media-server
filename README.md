# How to turn an Android TV Box or Phone into a Media Server

## 1. Introduction

- If you have an Android TV box for media playback or an android phone, you can turn it into a media server.
- I don't recommond using a a phone, because you have to keep it plugged in 24/7, this might bloat the battery unless you have the options to limit the charging percentage.
- We're gonna set this Android TV media server with a cheap box from Aliexpress, 4GB of ram, 32GB internal storage, and a USB 3.0 port. Depending on your needs, you can use the internal storage only, or attach an external large drive to the USB 3.0/2.0 port.
- We'll call the Android TV box used to stream media to other devices and to itself **server**
- We'll call an Android phone used to control the Android TV Box apps **remote**
- Make sure the **server** and **remote** are connected to the same network, wifi or ethernet. The **remote** phone can't be on 4G/5G during the setup.

## 2. Apps

### 2.1. APKs

- On the **server**, go to https://emby.media/server-android.html and download the apk.

Install the following apps

### 2.2. Google Play Store

- **tTorrent Lite** *Optional* in case all your media is in the external drive or transferred internally*
- **FTP Server (Multiple Users)** *Optional If you want to be able to move the files around on the server remotely*
- **Emby Player** *Optional* if you want to play media on the same TV Box/Android Phone. You have to either pay $5 for app, or purchase an Emby Server Subscription.

## 3. Setup Instructions

### 3.1. Reserve the server ip address

If you don't reserve the **server** ip address, it'll change each time you turn it off/on, and you'll have to figure it out each time.

1. Open the settings on your **server**, and depending on your device, you have to locate the mac address. It might under `About phone` > `Detailed info and specs` > `Status`
2. Open your router configuration url, check the back of it, most likely http://192.168.x.1, and enter username/password. Again, check the back of the router or look online for your device's model.
3. Locate the DHCP server, and reserve an ip address for the mac address, let's use 192.168.1.80

### 3.2. tTorrent Lite

1. Launch `tTorrent Lite`, it'll prompt you to select a download folder, we're gonna choose the folder `Movies` on the external/internal storage.
2. Tab on the three stripes > `Settings`:
3. Directories: You can change the download folder = `Set save directory`.
4. Limits: Enable `Start added torrents`. I prefer to `Set max. active downloads` to 1, and Enable `Sequential  download by default`, this way you can start playing the videos after 5-10% is downloaded. Most Android TV Boxes ethernet port is 100M only, so set the `Upload limit` less than 100M and/or lesser than your total upload speed. You can set `Enable share ratio limit` and set it to 0.1 or 1 or 2 if you have a limited data cap.
5. Network settings, open the Listening port in your router if you don't have UPnP enabled. Enable `uTP`. Check if the port is open at [canyouseeme](http://canyouseeme.org). I think you can install a VPN on the **server** and set to always on and block all connections if it's not connected. You have to choose one that supports port forwarding.
6. Interface: Enable `Web interface`, and set authentication if needed.
7. Power management: Enable `Start at boot` and `Force start at boot`. This way you don't have to start it manually each time you turn the **server** on.

### 3.3. Emby Server for Android

1. On the **server**, use the files explorer to locate the Emby Server for Android apk, Install it, and Launch the **Emby Server** app.
2. On the **remote, launch a web browser, enter your **server** ip address, here http://192.168.1.80:8096
3. Create a new user and password, add a library
  - Content type: Mixed content (tTorrent doesn't have a settings to choose a different folder for each torrent from the WebUI)
  - Keep `Enable real time monitoring` enabled
  - Add any metadata fetchers you like.
  - Disable: Save downloaded subtitles into media folders. So when you delete the torrent from **tTorrent lite**, there are no leftover files.
4. On the main interface, click on the wheel icon in the top right > `Users` > Select the new user/any other user > disable `Allow audio transcoding, if necessary, during media playback` and disable `Allow video transcoding, if necessary, during media playback`

### 3.4. Battery optimization

Disable battery optimization for **tTorrent Lite**, **Emby Server**, and optionally **FTP Server (Multiple Users)**

## 4. Usage

- On your **remote** install `transdrone`. Or you can use the WebUI http://192.168.1.80:1080
- Go to `Settings` > `Add new server` > `Add normal, custom server`:
  - Name = Android TV
  - Server type = tTorrent
  - IP or host name: 192.168.1.80 or 127.0.0.1 if it's on the same device tTorrent is installed.
  - User name & Password
  - If you changed the port from 1080, or didn't use authentication, tab on `Adavnced settings` > Change `Port number` and/or check `Disable authentication`
- Search your favorite tracker, copy the *magnet link* the *.torrent file download link*, or the *.torrent file*. **Disclaimer: USE LEGALLY OBTAINED MEDIA ONLY**
- On **transdrone**, click on the `+` sign, choose `file` and browse for the file or `link` symbol and paste the link.
- Let the download finish, it should appear in Emby Server.

Make sure to turn the **server** off then on at least once, wait for about 1 minute, and make sure the **tTorrent lite** and **Emby Server** links http://192.168.1.80:1080 and http://192.168.1.80:8096 work. This means the apps are launching at boot in the background without the need for user interaction.

### 5. Playback Benchmarks

- On phones and Android TV, install the Emby client app. (Sorry, I don't have an iOS device to benchmark).
- On PC, enter the webui address: http://192.168.1.80:8096
- Emby uses the hardware decoders of your device, and falls back to software decoders if it can't find one.
- The biggest problem is with Android phones, if they don't have a hardware decoder, the playback can be choppy depending on how powerful your chip, and and it'll consume a lot of energy.
- There are 3 codecs and 2 color depths to be aware of:
  - H264/x264: this is an old codec, and the most supported one, it'll play fine on any device 99.99% of the time.
  - HEVC/h265/x265: a better codec, but had licensing isues, so it's support is a mess.
  - AV1: the newest codec. Support is not very good on old devices. Software decoding is demanding and depends on your device power.
  - 8bit depth. The default one. Supported everywhere.
  - 10bit depth. Usually comes with h265 encodes, this is the one that gave me the biggest trouble on midrange and lowend devices.
- For audio codecs, I only had problems with E-AC3.
- **So stick to H264 8bit and AAC encodes and you'll be to direct play on all devices without transcoding.**
