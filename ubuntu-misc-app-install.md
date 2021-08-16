## Slack

Using snap manager with command:

```bash
sudo snap install slack --classic
```

## Autokey

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

After installation, using the existing backup key configs: 
- clone the data from repository
- create an empty folder or phrase/script in the autokey GUI. This step is important, or the application will not recognize the backup data folder. 
- delete the data folder under ~/.config/autokey
- Create a symbolic link to the backup **data** folder under home folder:
    ```bash
    ln -s ~/Workspace/personal-template/keyboard-mapping/autokey/data data
    ```

## xdotool and xbindkeys

The autokey has a most important missing feature is: it cannot capture mouse click as hotkey trigger. We can use xdotool and xbindkeys to fix this issue.

- Install the application through:
    ```bash
    sudo apt install xdotool xbindkyes
    ```
- clone the xbindkey config file from repo, if create a file by yourself, create an file **.xbindkeysrc**, add the following content:
    ```bash
    # mouse left click to trigger special comb: ctrl+alt+shift+1                               
    # then will be captured by autokey to simulate a mouse click event
    # Since the xdotool has a cooldown overhead for xorg, so manually add the sleep to reset
    "xdotool sleep 0.2 keydown Ctrl click 1 keyup Ctrl"
    alt + b:1
    ```
- create a symbolink under home folder and link it to the config file: `ln ~/Workspace/personal-template/keyboard-mapping/xbindkeys/.xbindkeysrc ~/.xbindkeysrc`
- stop all existing xbindkey service: `killall -s1 xbindkeys`
- restart the service: `xbindkeys -f ~/.xbindkeysrc`