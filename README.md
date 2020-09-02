# Clevis Mount Helper

## Dependencies

Install the `clevis` and `clevis-luks` packages.

`yum install clevis clevis-luks` or
`apt-get install clevis clevis-luks`
depending on your distro.

## Setup

Copy `clevis-mount.service` to `/etc/systemd/system`.

`sudo cp ./clevis-mount.service /etc/systemd/system/clevis-mount.service`

Copy `clevis-mount-helper` to `/etc/clevis-helper`.

`sudo mkdir /etc/clevis-helper
sudo cp ./clevis-mount-helper /etc/clevis-helper/clevis-mount-helper`

## Configuration

Clevis Mount Helper uses a configuration file `/etc/clevis-helper/clevistab` to configure its mount
operations. `clevistab` uses identical syntax to the `etc/fstab` file. On a single line in specify the
following arguments in order (delimited by whitespace): Device,  Mount point, File system type and
mount Options. The final 2 fstab arguments (dump and fsck) are ignored by the helper and can be
omitted. Device must be device that has been luks protected and bound with a clevis pin (
`clevis luks bind -d <device> <pin> '{}'`).
