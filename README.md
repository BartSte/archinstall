# README

Scripts for installing arch.

The following is assumed:

- You booted with a live USB.
- Your boot mode is UEFI.
- Your UEFI bitness is 64-bit.
- You have setup an internet connection.

If you do not understand any of the above, please follow the [official
installation guide](https://wiki.archlinux.org/index.php/Installation_guide).
instead of using these scripts.

## Usage

Download the install script using `curl`:

```bash
curl -O https://raw.githubusercontent.com/BartSte/archinstall/main/install 
```

Next, run the script with the arguments you want. For example:

```bash
bash install /dev/sda my-hostname
```

which will install arch on `/dev/sda` and set the hostname to `my-hostname`.

## Credits

- This repo was inspired on [auto-usb-arch-scripts](https://github.com/naelstrof/auto-usb-arch-scripts).
- The `aufii` script was copied from [auto-UEFI-entry](https://github.com/de-arl/auto-UEFI-entry).
