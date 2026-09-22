<div align="center">

# dotfiles ⌁

**a small, opinionated corner of my terminal**

`zsh` · `starship` · `nvm` · fewer repeated keystrokes

<br>

<sub>🪩 tuned for daily work &nbsp;·&nbsp; 🐚 kept deliberately small</sub>

</div>

![Desktop screenshot with the dotfiles configuration](screenshots/desktop.png)

---

```text
dotfiles/
└── zsh/
    └── .zshrc    shell options, completion, aliases & plugins
```

### What lives here

- shared, deduplicated shell history
- [Nord rice for Debian/XFCE](debian/rice/nord/README.md), including a Rofi launcher
- fuzzy and case-insensitive completion
- [Starship](https://starship.rs/) prompt initialization
- Zsh autosuggestions and syntax highlighting
- NVM bootstrap and a handful of workflow aliases

### XFCE shortcuts

The [XFCE shortcut backup](xfce/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-keyboard-shortcuts.xml) includes `Super+B` to open Chrome and `Super+C` to send `Ctrl+W` to the focused application. The latter uses the [close-tab script](xfce/.local/bin/fechar-aba) on X11.

To restore these two shortcuts from the repository root in an XFCE session:

```sh
install -Dm755 xfce/.local/bin/fechar-aba ~/.local/bin/fechar-aba
xfconf-query -c xfce4-keyboard-shortcuts -p '/commands/custom/<Super>b' -n -t string -s google-chrome
xfconf-query -c xfce4-keyboard-shortcuts -p '/commands/custom/<Super>c' -n -t string -s "$HOME/.local/bin/fechar-aba"
```

### Put it to work

```sh
git clone https://github.com/ArthurBufon/dotfiles.git ~/dotfiles
ln -s ~/dotfiles/zsh/.zshrc ~/.zshrc
exec zsh
```

> [!NOTE]
> The config contains aliases tied to my local project paths. Read it before linking and make those paths your own.

<details>
<summary><strong>Things the shell expects</strong></summary>

<br>

- Zsh
- GNU `dircolors`
- [Starship](https://starship.rs/)
- [zoxide](https://github.com/ajeetdsouza/zoxide) (`sudo apt install zoxide` no Debian)
- [`zsh-autosuggestions`](https://github.com/zsh-users/zsh-autosuggestions)
- [`zsh-syntax-highlighting`](https://github.com/zsh-users/zsh-syntax-highlighting)
- NVM, if Node version management is needed

</details>

---

<div align="center">
  <sub>Personal machinery. Borrow what fits; leave the rest. ◌</sub>
</div>
