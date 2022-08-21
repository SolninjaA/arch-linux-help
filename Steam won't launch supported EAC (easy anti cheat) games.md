## Steam won't launch supported EAC (easy anti cheat) games
#### This is the fix that worked for me, this is only applicable to people who have Fall Guys on Steam. If you want to get the free to play version from Epic Games follow this guide courtesy of the people at Heroic Games Launcher https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/wiki/FallGuys

I tried a lot to get this to work, what fixed it was actually installing the [**Flatpak**](https://wiki.archlinux.org/title/Flatpak) version of Steam. It turns out, some EAC games need a patched version of glibc and the Flatpak version of Steam automatically ships with that patched version.

#### Installing Flatpak and Steam
##### Requirements / reccomended packages to install:
Enable the [multilib](https://wiki.archlinux.org/title/Official_repositories#multilib) repository. (nano / vim `/etc/pacman.conf` and uncomment `#[multilib]` and `#Include = /etc/pacman.d/mirrorlist` so they don't have a `#` at the start of the line)

Installed 32-bit version [OpenGL graphics driver](https://wiki.archlinux.org/title/Xorg#Driver_installation). (https://wiki.archlinux.org/title/Xorg#Driver_installation, see `OpenGL (multilib)` section)

Generated [`en_US.UTF-8`](https://wiki.archlinux.org/title/Locale#Generating_locales) locale, preventing invalid pointer error. (nano / vim `/etc/locale.gen`, uncomment `en_US.UTF-8 UTF-8` and run `locale-gen`)

The GUI heavily uses the Arial font. [See Microsoft fonts](https://wiki.archlinux.org/title/Microsoft_fonts). An alternative is to use [ttf-liberation](https://archlinux.org/packages/?name=ttf-liberation) or [fonts provided by Steam](https://wiki.archlinux.org/title/Steam/Troubleshooting#Text_is_corrupt_or_missing) instead. (this isn't the only way, but I ran `sudo pacman -S lib32-fontconfig ttf-liberation wqy-zenhei`)

Install [wqy-zenhei](https://archlinux.org/packages/?name=wqy-zenhei) to add support for Asian languages. (this was done in the above command)

If using [systemd-networkd](https://wiki.archlinux.org/title/Systemd-networkd) for network management, install [lib32-systemd](https://archlinux.org/packages/?name=lib32-systemd) in order for Steam to be able to connect to its servers. (if you use systemd-networkd run `sudo pacman -S lib32-systemd`)

##### Commands (note: The below commands will run through an installation of Fall Guys. The steps should be the same across games as long as the game has implemented EAC in a way Steam can handle it. See https://areweanticheatyet.com/):

1. Run `sudo pacman -S flatpak`
2. Run `flatpak --user remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo`
3. Run `flatpak --user install flathub com.valvesoftware.Steam`
4. Run `flatpak run com.valvesoftware.Steam` (if you are having troubles with Asian fonts in game, try running Steam with `flatpak run --filesystem=~/.local/share/fonts --filesystem=~/.config/fontconfig  com.valvesoftware.Steam`)
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
15. <a id=optional-step-15> Optional Step - only applicable to people who haven't installed Fall Guys yet: At the top left select "Steam", "Settings", "Downloads" and click "Clear Download Cache"
16. If you haven't installed Fall Guys click on "Fall Guys" in your steam library and click "Install"
17. Once it is finished press "Play"

Hopefully Fall Guys is now installed and running! If it is not and you followed the above steps, try un-installing Fall Guys, clearing the download cache (<a href=#optional-step-15> see Optional Step 15 </a>) and then install Fall Guys again. Good luck!
#### Sources:
https://wiki.archlinux.org/title/Steam#Alternative_Flatpak_installation

https://wiki.archlinux.org/title/Steam#Proton_Steam-Play

https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/wiki/FallGuys

https://wiki.archlinux.org/title/Steam/Troubleshooting#Text_is_corrupt_or_missing

https://wiki.archlinux.org/title/Locale#Generating_locales

https://wiki.archlinux.org/title/Xorg#Driver_installation
