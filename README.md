# README

Scripts for installing arch.

The following is assumed:

- You booted with a live USB.
- Your boot mode is UEFI.
- Your UEFI bitness is 64-bit.

If you do not understand any of the above, please follow the [official
installation guide](https://wiki.archlinux.org/index.php/Installation_guide)
instead of using these scripts.

## Usage

After you booted into arch using a live USB, make connection to the internet.
You can plugin a network cable (not configuration neede), or you can use the
wifi. The latter needs some configuration using `iwctl` which is supplied by
the environment on the USB. Do the following

```bash
iwctl --passphrase=PASSPHRASE station DEVICE connect SSID
```

where `DEVICE` is the name of your wifi device (you can find it using `iwctl
device list`) for example `wlan0`, `SSID` is the name of your wifi network and
`PASSPHRASE` is the password of your wifi network.

Next, download the `install` script using `curl`:

```bash
curl -O https://raw.githubusercontent.com/BartSte/archinstall/main/install
```

Next, run the script with the arguments you want. For example:

```bash
bash install DISK HOSTNAME USERNAME
```

where `DISK` is the disk you want to install arch on (e.g. `/dev/sda`, you can
find it using `lsblk` or `fdisk -l`), `HOSTNAME` is the hostname you want to
give to your machine (e.g. mylaptop), and `USERNAME` is the username you want
to create. After running the script, the following will be done:

- 2 scripts will be downloaded from this repository: `configure`, `aufii`
  `visudo_editor`.
- The disk is partitioned and formatted with a GPT partition table with:
  - part 1, label "EFI system partition": 512MiB EFI partition (FAT32)
  - part 2, label "Swap partition": 4GiB swap partition (swap)
  - part 3, label "Root partition": 100% of the remaining space (ext4)
- The `configure` script is executed (which uses the other scripts) is executed
  on the new system using `arch-chroot`, which will configure the system.
- Later, `configure` executes `aufii` script which starts an interactive
  tool to generate the `efibootmgr` commands into an executable. The `aufii`
  script was not written by me (see [credits](#credits)).

After the script is done, you can reboot into your new system. You can login
using the username and password you provided. Note that you do not have wifi,
as this was only configured for the live USB environment. For convenience,
the package `networkmanager` is installed, so you can run `nmtui` to connect
to your wifi network.

## Credits

- This repo was inspired on [auto-usb-arch-scripts](https://github.com/naelstrof/auto-usb-arch-scripts).
- The `aufii` script was copied from [auto-UEFI-entry](https://github.com/de-arl/auto-UEFI-entry).
