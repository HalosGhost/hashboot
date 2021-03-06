**hashboot** hashes all files in `/boot` and the MBR to check them during early
boot. It is intended for when you have encrypted the root partition but not the
boot partition. The checksums and a backup of the contents of `/boot` are stored
in `/var/lib/hashboot` by default. If a checksum doesn't match, you have the
option to restore the file from backup.

If there is a core- or libreboot BIOS and [flashrom](https://flashrom.org/)
installed, **hashboot** can check the BIOS for modifications too.

We moved our code to
[schlomp.space](https://schlomp.space/tastytea/hashboot) but we keep the
[GitHub-repo](https://github.com/tastytea/hashboot) as a mirror.

# Install

## Packages

### Void Linux

``` shell
xbps-install -S hashboot
```

### Gentoo Linux

Ebuilds are available via the
[tastytea repository](https://schlomp.space/tastytea/overlay).

``` shell
emerge -a sys-apps/hashboot
rc-update add hashboot boot
```

### Arch Linux

Use the [package from AUR](https://aur.archlinux.org/packages/hashboot/).

## Manual

### Any distro

The releases on
[schlomp.space](https://schlomp.space/tastytea/hashboot/releases) are
PGP-signed. The key-ID is `F7301ADFC9ED262448C42B64242E5AC4DA587BF9`
(`242E5AC4DA587BF9`). You can fetch it with `gpg --locate-key
autosign@tastytea.de`.

* Make hashboot executable
* Place hashboot anywhere in ${PATH}
* Install the appropriate init script
* If applicable, copy `hooks/kernel-postinst` to /etc/kernel/post{inst,rm}.d/zzz-hashboot
(make sure it is called after all other hooks)
* To generate the manpage, install [asciidoc](http://asciidoc.org/) and run
`build_manpage.sh`.

# Usage

* First run creates a configuration file. Select the desired checkroutines
* Run `hashboot index` to generate checksums and a backup for /boot and MBR
* Run `hashboot check` to check /boot and MBR
* Run `hashboot recover` to replace corrupted files with the backup

# Notes

* You can't use the openrc/sysv init scripts with parallel boot.
* The systemd and SysVinit init scripts have not been tested in a while, but
will probably work.

# License

```PLAIN
"THE HUG-WARE LICENSE" (Revision 2):
teldra <teldra@rotce.de> and tastytea <tastytea@tastytea.de> wrote this.
As long as you retain this notice you can do whatever you want with this.
If we meet some day, and you think this is nice, you can give us a hug.
```
