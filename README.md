# dracut-uefi-simple
====

## About

`dracut-efi-simple` is a pacman hook intended to create a simple unified kernel image and backup the current one. Some of the work done here is based on [dracut-uefi-hook](https://aur.archlinux.org/packages/dracut-uefi-hook/) AUR package.

What this hook does:

- backs up `/efi/BOOT/Arch/linux-signed.efi` (if it exists) to `/efi/BOOT/Arch/linux-signed-bkp.efi`.
- generates a new image on  `/efi/BOOT/Arch/linux-signed.efi` .
- prints the current EFI bootlist.
- triggers image creation if any kernel/microcode/systemd related packages/paths are updated.

What this hook doesn't do:

The hook itself is not intended to do secureboot kernel image signing like [sbupdate](https://github.com/andreyv/sbupdate) neither I have the intention to make those distro-agnostic, configuration-oriented, etc. Some paths like `/efi/BOOT/Arch/` are fixed cause that's the standard i've adopted on my setups for the directories inside the `ESP`. Also, other distributions rely heavily on dracut to create inital ramdisks and most of those distro-specific scripts will make the dracut configuration example(below) error prone.

[This is](https://nwildner.com/posts/2020-07-04-secure-your-boot-process/) the usecase for `dracut-efi-simple` since i'm trying to replace `sbupdate`+`mkinitcpio` with pure `dracut`.

This hook will not handle `efibootmgr` automatic EFI entry creation tasks as well(see below).

## Dracut configuration.

See my example [here](examples/etc/dracut.conf.d/uefi.conf)

## Install

Make sure your user is able to `sudo`.

```
git clone https://github.com/nwildner/dracut-uefi-simple.git
cd dracut-uefi-simple
makepkg -si
```

Answer `y` and you are good to go. Whenever some key kernel related packages are updated, this hook will automatically run

## After installation

Double-check if you are able to create efi entries with `bootctl | grep -i 'boot loader sets'` then create EFI entries: 

```
efibootmgr -c -d /dev/sda -p 1 --label "Arch Backup" -l "BOOT\Arch\linux-signed-bkp.efi" --verbose
efibootmgr -c -d /dev/sda -p 1 --label "Arch" -l "BOOT\Arch\linux-signed.efi" --verbose
```

Replace `sda` with your disk name, and change `--label` to any name you want. The last entry created gets the boot priority and that's why backup image is added first.
