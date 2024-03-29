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

## Display Settings

- Solid color background (dark slate gray)

    ```bash
    gsettings set org.gnome.desktop.background picture-uri ""
    gsettings set org.gnome.desktop.background primary-color '#2F4F4F'    
    ```

## Terminal Settings

### configure oh-my-zsh

```bash
  sudo apt install zsh
  sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

### set zsh themes

- download resource

  ```bash
  git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
  ```

- Set `ZSH_THEME="powerlevel10k/powerlevel10k"` in `~/.zshrc`

### zsh plugins

- zsh-syntax-highlighting

  ```bash
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```

  - add the plugin to `~/.zshrc`
  
    ```bash
        plugins=([plugins...] zsh-syntax-highlighting)
    ```

- zsh-autosuggestions

  ```bash
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  ```
  
  - add the plugin to `~/.zshrc`
  
    ```bash
        plugins=([plugins...] zsh-autosuggestions)
    ```

- zsh-completions

  ```bash
  git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:=~/.oh-my-zsh/custom}/plugins/zsh-completions
  ```

  - add the plugin to `~/.zshrc`
  
    ```bash
        plugins=([plugins...] zsh-completions)
    ```

### change directory/folder color

```bash
git clone https://github.com/seebi/dircolors-solarized 
echo '\neval `dircolors dircolors-solarized/dircolors.256dark`\n' >> ~/.zshrc 
```

## CopyQ

```bash
sudo add-apt-repository ppa:hluk/copyq
sudo apt update
sudo apt install copyq
```

open the preferences, configure shortcut for `show main window under mouse cursor`


## disable system wide prompt "select to paste" from fcitx

symptom: when enter `ctrl+;", a window will prompt "select to paste" which is from fcitx. To disable this prompt, disable the shortcut in fcitx add-on.

![](images/fcitx-prompt-copy-to-paste.png)

![](images/fcitx-addon.png)  