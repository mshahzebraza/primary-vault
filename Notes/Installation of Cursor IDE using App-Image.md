---
categories:
- '[[TechLearning]]'
tags:
- linux-pc-setup
---
## Context
Linux has a [few ways to install programs](obsidian://open?vault=Obsidian%20Vault&file=Types%20of%20Linux%20Applications) mainly the [Deb and Snap packages](https://askubuntu.com/questions/1029610/if-a-package-is-available-as-both-a-deb-and-a-snap-which-method-is-preferrable). However, a recent type of installation is the use of 'App Images', which are basically executable files right after the download and contain all the dependencies within them. This allows them with the convenience of using the Image on any Linux distribution.

> Theoretically, it sounds similar to what docker offers.

## Installation
1. Install the App Image from the cursor website. I'd prefer installation using `snap`/`apt` but there is no other installation method than the `App-Image`. 
2. After the installation, we can just go to the place of download and try opening it and it should work. However, by default, Linux might not allow this and we might have to execute a script to change the permissions.
```sh
chmod +x cursor-0.42.4x86_64.AppImage
```
   This allows to run the app-image with correct permissions.

3. **(optional).** I didn't face regarding the need of `FUSE` to run. However, if such an error is thrown then install `libfuse2` via this command
```sh
sudo apt-get install libfuse2
```
4. Now run the AppImage by just executing the path of the AppImage.
```bash
./you-cursor-app.AppImage
```
OR
```
./you-cursor-app.AppImage --no-sandbox
```
   
   Moreover, when trying to run the image using the terminal instead of `Files`/`Files Manager`, we might get an error regarding sandbox.
   While, the error itself suggests making sure that the permission access of a specific directory needs to be changed. But when I tried that, It said no such directory/path found.
   So, I just went with the more convenient option of using the `--no-sandbox` flag after the original command `./your-cursor-app.AppImage`. To run the app, just type in the path of the app with the no-sandbox flag. 
   
This should be good enough to start the cursor app-image. 

## Access app via App Menu

However, there is a certain inconvenience of not being able to search in the app-menu, or not having the cursor app in the docks. This feature comes enabled for all the applications installed via `snap`/`apt` but for the app-images we have to do certain configuration.

1. Move the app to the `/opt` directory. So the new file path should be something like `/opt/cursor.appimage`. You can choose to name it differently but then all the other references should match the path.
   The moving is done by the following command. (Assuming it was downloaded from browser into `~/Downloads` directory with the name of `cursor.AppImage`)
```sh
mv ~/Downloads/cursor.AppImage /opt/cursor.appimage
```

> Normally `opt` directory is for optional programs and custom app-image installs make sense to be placed here. However, this step doesn't do anything to allow the App-Menu to read the cursor application

2. To allow the Ubuntu App Menu to read the Cursor Application, we have to create a `cursor.desktop` configuration file and place it in a specific directory `/usr/share/applications`. 
   To avoid navigating to the path and creating a file manually, run this script.
   
```
sudo nano /usr/share/applications/cursor.desktop
```

4. The contents of the `cursor.desktop` file are as follows.
```
[Desktop Entry]
Name=Cursor AI IDE
Exec=/opt/cursor.appimage --no-sandbox
Icon=/opt/cursor.png
Type=Application
Categories=Development;
```

- You must have noticed the Icon Image, which you can download form Github/Linkedin of Cursor and must then be moved to the `/opt` directory besides the app-image.
- Another thing is that the `--no-sandbox` flag is also added here since for me, I couldn't use the app-image without this flag and that's why `--no-sandbox` should be added to the `Exec` command. You can skip it if it works without it.
Once edited the file with the correct contents save and exit.

5. Try restarting the PC and you should be able to search the Cursor from the App Menu. Otherwise, try to copy the `cursor.desktop` file to Desktop by using the following command and restart. After that you should be good to go
   
```sh
cp /usr/share/applications/cursor.desktop ~/Desktop/cursor.desktop
```
