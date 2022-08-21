# Arch / Linux help
A repository for issues I have come across during my time in Arch Linux, and fixes for them. Granted, veteran Arch / Linux users may find these problems / fixes obvious.

## Steam won't launch supported EAC (easy anti cheat) games
#### This is the fix that worked for me, this is only applicable to people who have Fall Guys on Steam. If you want to get the free to play version from Epic Games follow this guide courtesy of the people at Heroic Games Launcher https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/wiki/FallGuys

I tried a lot to try and get this to work, what fixed it was actually installing the **Flatpak** version of Steam. It turns out, some EAC games need a patched version of glibc and the Flatpak version of Steam automatically ships with that patched version.

#### Installing Flatpak and Steam
##### Requirements / reccomended packages to install:
Enable the multilib repository and install the steam package.

The following requirements must be fulfilled in order to run Steam on Arch Linux:

Installed 32-bit version OpenGL graphics driver. (https://wiki.archlinux.org/title/Xorg#Driver_installation, see OpenGL (multilib) section)

Generated en_US.UTF-8 locale, preventing invalid pointer error. (nano / vim `/etc/locale.gen`, un-comment `en_US.UTF-8 UTF-8` and run `locale-gen`)

The GUI heavily uses the Arial font. See Microsoft fonts. An alternative is to use ttf-liberation or fonts provided by Steam instead. (this isn't the       only way, but I ran `sudo pacman -S lib32-fontconfig ttf-liberation wqy-zenhei`

Install wqy-zenhei to add support for Asian languages. (this was done in the above command)

If using systemd-networkd for network management, install lib32-systemd in order for Steam to be able to connect to its servers. (if you use systemd-       networkd run `sudo pacman -S lib32-systemd`

##### Commands (note: the below commands will run through an installation of Fall Guys, the steps should be the same across games):

1. Run `sudo pacman -S flatpak`
2. Run `flatpak --user remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo`
3. Run `flatpak --user install flathub com.valvesoftware.Steam`
4. Run `flatpak run com.valvesoftware.Steam` (if you are having troubles with Asian fonts in game, run `flatpak run --filesystem=~/.local/share/fonts --filesystem=~/.config/fontconfig  com.valvesoftware.Steam`)
5. Run `paru/yay/aurhelper -S protonup-qt`
6. Make sure Steam is not open
7. Run `protonup-qt`
8. At the top of the GUI where it says "Install for:" click the dropdown and select "Steam Flatpak"
9. Near the bottom left select "Add version:
10. Make sure underneath where it says "Compatability tool:" it says "GE-Proton"
11. Make sure underneath "Version:" it says GE-Proton7-15 (it may work with versions newer than 15, however I tested 15 and it worked for me)
12. Click "Install"
13. Once the installation is done open Steam
14. If you haven't already installed Fall Guys right click Fall Guys and select "Compatability". In the dropdown select GE-Proton7-15 (or whatever version you chose)
Optional Step- only applicable to people who haven't installed Fall Guys yet: At the top left select "Steam", "Settings", "Downloads" and click "Clear Download Cache"
15. If you haven't installed Fall Guys click on "Fall Guys" in your steam library and click "Install"
16. Once it is finished press "Play"

Hopefully Fall Guys is now installed and running! If it is not and you followed the above steps, try un-installing Fall Guys, clearing the download cache (see Optinal Step) and installing Fall Guys again. Good luck!
#### Sources:
https://wiki.archlinux.org/title/Steam#Alternative_Flatpak_installation

https://wiki.archlinux.org/title/Steam#Proton_Steam-Play

https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/wiki/FallGuys

https://wiki.archlinux.org/title/Steam/Troubleshooting#Text_is_corrupt_or_missing

https://wiki.archlinux.org/title/Locale#Generating_locales

https://wiki.archlinux.org/title/Xorg#Driver_installation



## The SUID sandbox helper binary was found, but is not configured correctly. Rather than run without sandboxing I'm aborting now. You need to make sure that /path/ is owned by root and has mode 4755.
#### The fix that worked for me
Run `sysctl kernel.unprivileged_userns_clone=1` in the terminal. You may have to run it with `sudo`.

`sudo sysctl kernel.unprivileged_userns_clone=1`

#### Sources:
https://github.com/electron/electron/issues/17972
