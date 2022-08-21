## The SUID sandbox helper binary was found, but is not configured correctly. Rather than run without sandboxing I'm aborting now. You need to make sure that /path/ is owned by root and has mode 4755.
#### The fix that worked for me
Run `sysctl kernel.unprivileged_userns_clone=1` in the terminal. You may have to run it with `sudo`.

`sudo sysctl kernel.unprivileged_userns_clone=1`

Note: you would have to run this command every time you turn on your computer (at least in my experience). You could try adding `exec sysctl kernel.unprivileged_userns_clone=1` in your `~/.xinitrc` file (I haven't tested this yet), adding `sysctl kernel.unprivileged_userns_clone=1` as a command that runs on startup in your window manager or creating a script that runs on startup.

#### How to create a script that runs on startup
1. Run `sudo nano/vim /etc/systemd/system/whatYouWantToCallTheService.service`
2. Paste the following:
```
[Unit]
Description=your description

[Service]
ExecStart=sysctl kernel.unprivileged_userns_clone=1

[Install]
WantedBy=multi-user.target
```
3. Run `sudo systemctl enable whatYouWantToCallTheService.service`

#### Sources:
https://github.com/electron/electron/issues/17972

https://www.linuxuprising.com/2021/12/how-to-run-command-or-script-as-root-on.html
