# Vagrant Box: Manjaro-i3 Linux 16.06 (64-bit) 

* Name: [mloskot/manjaro-i3-16.06](https://atlas.hashicorp.com/mloskot/boxes/manjaro-i3-16.06/)
* Version: 1.0.0
* Download: https://github.com/mloskot/vagrant-boxes/releases/download/manjaro-i3-16.06-v1.0.0/manjaro-i3-16.06-v1.0.0.box

A minimal base box built for Vagrant from
[Manjaro i3 16.06](https://forum.manjaro.org/t/manjaro-i3-16-06/3329)
using VirtualBox 5.0.21 and packaged using Vagrant 1.8.1.

The box was built using 
[manjaro-i3-16.06-x86_64.iso](https://sourceforge.net/projects/manjarolinux/files/community/i3/16.06/)
according to canonical Vagrant way.

## Box VM

* CPU: 2
* RAM: 2048 MB
* VHD: 40 GB
* Network:
  * NAT
  * SSH via port fowarding: host `2222` to guest `22`
* Users
  * `root / vagrant`
  * `vagrant / vagrant` (Public Key authentication, password-less `sudo`)

## Box Software

A default Manjaro i3 installatios with a few extras:

* [dwb](http://portix.bitbucket.org/dwb/) - a lightweight web browser. 
* Firefox
* Git with Bash completion and prompt configured.
* [i3](https://i3wm.org) - a lightweight window manager, pre-configured with `jkl;` motion keys.
* Thunar - a lightweight file manager.
* Vim - pre-configured with `jkl;` motion keys.
* VirtualBox Guest Addition 5.0.20:
  * [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils)
  * [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch)
* Visual Studio Code
* [Vundle](https://github.com/VundleVim) plug-in manager for Vim with a few handy plugins.

Chris Kempson's [Monokai](https://chriskempson.github.io/base16/#monokai)
color scheme configured for
[urxvt](https://wiki.archlinux.org/index.php/rxvt-unicode) and Vim.

## Box Usage

* `vagrant init mloskot/manjaro-i3-16.06`
* Enable GUI in the generated Vagrantfile by uncommenting:
```
  config.vm.provider "virtualbox" do |v|
    v.gui = true
  end 
```
* `vagrant up --provider virtualbox`

Alternatively, use `Vagrantfile` from GitHub
```
git clone https://github.com/mloskot/vagrant-boxes.git
cd manjaro-i3-16.06-x86_64
vagrant up
```

## Troubleshooting

### Disabling Win+Enter Narrator hotkey in Windows

In Windows, `Win+Enter` keybinding launches the Windows Narrator.
Windows key is a popular alternative [i3 modifier](https://i3wm.org/docs/userguide.html#_using_i3)
(`$mod`) key and pressing `$mod+Enter` opens a new terminal.
The annoyance of launching the Windows Narrator every time
you aim to open a terminal in the i3 environment of the guest VM,
can be avoided by disabling the `Win+Enter` as the Narrator hotkey:

1. Create registry key ` HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT \CurrentVersion\Image File Execution Options\Narrator.exe`
2. Create new String Value with name `Debugger` and value `%1`.