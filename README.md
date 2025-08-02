# How to turn an Android TV or Phone into a Media Server

- If you have an Android TV box for media playback on TV or even an extra android phone, you can turn it into a media server with torrents.
- I don't recommond using a a phone, because you have to keep it plugged on 24/7, this might bloat the battery. Unless you have the options to limit the charging percentage.
- We're gonna set this Android TV media server with a cheap box from Aliexpress, 4GB of ram, 32GB of internal storage, and a USB 3.0 port. Depending on your needs, you can use the internal storage only, or attach an external large drive to the USB 3.0/2.0 port for more content.
- We'll call the Android TV box used to stream media to other devices and to itself **Server**
- We'll call an Android Phone used to control the Android TV Box **Remote**
- Make sure the **server** and **remote** are connected to the same network, wifi or ethernet. the **remote** phone can't be on 4G/5G during the setup.

---

## 1. Apps

Install the following apps

### 1.1. Google Play Store

- **Cx File Explorer**
- **tTorrent Lite** *Optional* if you all your media in the external drive or transfer it internally*
- **FTP Server (Multiple Users)** *Optional If you want to be able to move the files around*
- **Emby Player** *Optional* if you want to play media on the same TV Box/Android Phone. But you have to either pay $5 for app, or purchase a server license.

### 1.2. APKs

- On the **remote**, go to [Android Server for Android](https://emby.media/server-android.html) and download the apk.

---

## 2. Setup Instructions

## 2.1. Reserve the ip address

1. Open the settings on your **Server**, and depending on your device, you have to locate the mac address. It might under `About phone` > `Detailed info and specs` > `Status`
2. Open your router configuration url, check on the back of it. Most likely http://192.168.x.1, and enter username/password. Again, check the back of the router or look online for your device's model.
3. Locate the DHCP server, and reserve an ip address for the mac address, let's use 192.168.1.80

### 2.2. tTorrent Lite

1. Launch `tTorrent Lite`, it'll prompt you to select a download folder, we're gonna choose the folder `Movies` on the external storage, you can also use the internal storage.
2. Tab on the three stripes > `Settings`:
3. Directories: You can change the download folder = `Set save directory` here.
4. Limits: Enable `Start added torrents`. I prefer to `Set max. active downloads` to 1, and Enable `Sequential  download by default`, this way you can start playing the videos after 5-10% is downloaded. Most Android TV Boxes ethernet port is 100M only, so I like to set an `Upload limit` of less than 100M and/or less than the total upload of my bandwidth. You can set `Enable share ratio limit` if you have a limited data cap.
5. Network settings, open the Listening port in your router if you don't have UPnP enabled. Enable `uTP`. Check if the port is open at [canyouseeme](http://canyouseeme.org) 
6. Interface: Enable `Web interface`, and set authentication needed.
7. Power management: Enable `Start at boot` and `Force start at boot`. This way you don't have to start it manually each time you turn the **server** on.

### 2.3. Emby Server for Android

1. Launch `Cx File Explorer` on the **server**, go to `network tab`, tab on `Access from network`. This app will make the first installation easy.
2. Install `Cx File Explorer` on the **remote**, go to the `network tab`, tab on `New location` > `Remote` > `FTP` and enter the `ip address`, `port`, select `FTP`, and enter `Username` and `Password` from the launched FTP server. Now copy the Emby Server for Android apk to **Server** Download folder.
3. On the **Server**, quit the FTP server in `CX File Explorer`, go to `LOCAL` > `Main Storage` > `Download` and install the Emby Server for Android apk. You might need to give Cx File Explorer permissions to install apps from unknown sources.
4. Launch the **Emby Server** app.
5. On the **remote, launch a web browser, enter your **server** ip address, here http://192.168.1.80:8096
6. Create a new user and password, add a library
  - Content type: Mixed content (tTorrent doesn't have a settings to choose a different folder for each torrent from the WebUI)
  - Add any metadata fetchers you like.
  - Disable: Save downloaded subtitles into media folders. So when you delete the torrent from **tTorrent lite**, there are no leftover files.

### 2.4. Battery optimization

Disable battery optimization for **tTorrent Lite**, **Emby Server**, and optionally **FTP Server (Multiple Users)**

## 3. Usage

- On your **remote** install `transdrone`
- Go to `Settings` > `Add new server` > `Add normal, custom server`:
  - Name = Android TV
  - Server type = tTorrent
  - IP or host name: 192.168.1.80 or 127.0.0.1 if it's on the same device tTorrent is installed.
  - User name & Password
  - If you changed the port from 1080, or didn't use authentication, tab on `Adavnced settings` > Change `Port number` and check `Disable authentication`
- Search your favorite tracker, copy the *magnet link* the *.torrent file download link*, or the *.torrent file*.
- On **transdrone**, click on the `+` sign, choose `file` or `link` symbol. And browse for the file or paste the link. **USE LEGALLY OBTAINED MEDIA ONLY**
- Let the download finish, it should appear in Emby Server.

Make sure to turn the **server** off then on, wait for about 1 minute, and make sure the **tTorrent lite** and **Emby Server** links work.

### 4. Playback
