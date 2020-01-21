## Slack

Using snap manager with command:

```bash
sudo snap install slack --classic
```

# Autokey

Download autokey from the [release page](https://github.com/autokey/autokey/releases/). Yes, there is no PPA configuration. And remember to download the **common** package and the **version being installed** (qt version hear).

Then using the command to install:

```bash
sudo dpkg --install autokey-common_xxx_all.deb autokey-qt_xxx_all.deb
```

Afterwards, you may see some missing packages complaints, using the following instructions to fix the dependencies

```bash
sudo apt --fix-broken install
```

More details can refer the [official wiki](https://github.com/autokey/autokey/wiki/Installing#installation-options).

After installation, move the backup configurations to folder `$HOME/.config/autokey`