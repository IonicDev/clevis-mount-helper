# Clevis Mount Helper

Clevis Mount Helper provides a means of automatically mounting luks encrypted clevis bound devices
that does not rely on clevis-luks-askpass.path and fstab and crypttab support for \_netdev. This
solution only supports automounting of non root volumes.

## Dependencies

Install the `clevis` and `clevis-luks` packages.

`yum install clevis clevis-luks` or
`apt-get install clevis clevis-luks`
depending on your distro.

## Setup

Copy `clevis-mount.service` to `/etc/systemd/system`.

`sudo cp ./clevis-mount.service /etc/systemd/system/clevis-mount.service`

Copy `clevis-mount-helper` to `/etc/clevis-mount-helper`.

`sudo mkdir /etc/clevis-mount-helper
sudo cp ./clevis-mount-helper /etc/clevis-mount-helper/clevis-mount-helper`

## Configuration

Clevis Mount Helper uses a configuration file `/etc/clevis-mount-helper/clevistab` to configure its
mount operations. `clevistab` uses identical syntax to the `etc/fstab` file. In `clevistab` on a
single line for each luks device specify the following arguments in order (delimited by whitespace):
Device,  Mount point, File system type and mount Options. The final 2 fstab arguments (dump and
fsck) are ignored by the helper and can be comitted. Device must be device that has been luks
protected and bound with a clevis pin (`clevis luks bind -d <device> <pin> '{}'`).
