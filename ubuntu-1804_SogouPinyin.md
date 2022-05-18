# Ubuntu 18.04 Initial Config After 

## Sogou Pinyin

### Notes for Ubuntu 22.04

- Follow the official website for installation
- after installation debian package, set the `/etc/environment` to solve compatibility issue. See [this thread](https://askubuntu.com/questions/1406597/how-to-get-sogou-pinyin-ime-work-properly-in-ubuntu-22-04).
  
  ```bash
    GTK_IM_MODULE=fcitx
    QT_IM_MODULE=fcitx
    XMODIFIERS="@im=fcitx"
  ```

1. Uninstall ibus

    ```bash
    sudo apt remove ibus
    ```

2. Cleanup ibus config

    ```bash
    sudo apt-get purge ibus
    ```

3. uninstall keyboard indicator from top task bar

    ```bash
    sudo  apt-get remove indicator-keyboard
    ```

4. install fcitx

    ```bash
    sudo apt install fcitx-table-wbpy fcitx-config-gtk
    ```

5. switch default input method to fcitx

    ```bash
    im-config -n fcitx
    im-config
    sudo reboot
    ```

6. Download Sogou Pinyin deb package

7. Install

    ```bash
    sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb
    ```

8. Fix damaged package

    ```bash
    sudo apt-get install -f
    ```

9. Cancel Appearance for better compatibility

    ```bash
    fcitx-config-gtk3
    ```

    * `Configure>>Addon>>Advanced>>Classic`

10. Disable the `Extra key for trigger input method` to avoid shift trigger input method switch. To do this, open configuration through input method menu or with command `fcitx-config-gtk3`
    * Global Config Tab->Choose `Disable` for `Extra key for trigger input method`

11. Fcitx will overwrite the original setting with default one from time to time, use the following command to make the fcitx config file **immutable**.

    ```bash
    sudo chattr +i ~/.config/fcitx/config
    ```
