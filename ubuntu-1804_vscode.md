# Configurations for VSCode on Ubuntu

## Installation

Using snap manager with command:

```bash
sudo snap install --classic code # or code-insiders
```

## unlock "ALT" related shortcuts

To enable the alt related shortcuts, alt triggered menu(mnemonics in GTK) need to be disabled. In VSCode settings, disable [`window.enableMenuBarMnemonics`]((https://code.visualstudio.com/updates/v1_13#_disable-menu-bar-mnemonics))

## Enable Windows/Super Key

-   The settings of keyboard layout is not visible by default in Ubuntu 18.04+, install tweaks to set advance layout. And in `Alt/Win key behavior`, enable `Hyper is mapped to win`. That will also unlock the super key for **IntelliJ**
