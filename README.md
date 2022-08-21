# Arch / Linux help
A repository for issues I have come across during my time in Arch Linux, and fixes for them. Granted, veteran Arch / Linux users may find these problems / fixes obvious.

## The SUID sandbox helper binary was found, but is not configured correctly. Rather than run without sandboxing I'm aborting now. You need to make sure that /path/ is owned by root and has mode 4755.
#### The fix that worked for me
Run `sysctl kernel.unprivileged_userns_clone=1` in the terminal. You may have to run it with `sudo`.

`sudo sysctl kernel.unprivileged_userns_clone=1`
