# Ubuntu 18.04 Initial Config After 

## Sogou Pinyin
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
4. install fxitx
```bash
sudo apt install fcitx-table-wbpy fcitx-config-gtk
```
切换为 Fcitx输入法
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
Configure>>Addon>>Advanced>>Classic

