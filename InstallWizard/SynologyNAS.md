# As a Python package
This is the recommended method as it mirrors how you would install FlexGet on just about any other system. You will need to be logged into the Synology NAS as root to install packages.

## `opkg`
The first step is to install `opkg`, the best package manager around for embedded systems like your NAS. Follow the instructions at:

[https://github.com/Entware-ng/Entware-ng/wiki/Install-on-Synology-NAS](/https://github.com/Entware-ng/Entware-ng/wiki/Install-on-Synology-NAS)

## System dependencies
You'll need to install Python and pip:

```
$ opkg install python3
$ opkg install python3-pip
```

## Transmission
It is highly recommended that you use the Transmission BitTorrent client instead of the built-in client. Transmission can also be installed via `opkg`.

```
$ opkg install transmission-daemon
$ opkg install transmission-web
```

## Next
You're ready to [install FlexGet](/InstallWizard/SynologyNAS/FlexGet).

  

# Using the synocommunity package
The synocommunity repository [https://synocommunity.com/](/https://synocommunity.com/) includes a FlexGet package. If you are less comfortable with the command line, you will probably find this method easier. It may, however, be more difficult to maintain. You must also wait for the package maintainers to update the FlexGet package; with the above method, updates to FlexGet may be installed as soon as they are released.

Follow the homepage instructions to add synocommunity to your NAS, and then install Python and FlexGet through the web interface. The config file will be available at `/usr/local/flexget/var/config.yml`.
