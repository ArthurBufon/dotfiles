# Rice Nord para Debian + XFCE

Rice escuro, limpo e discreto para Debian 13 com XFCE em X11. A base é a paleta Nord: fundo `#2E3440`, texto claro e acentos azulados. O foco é em um desktop agradável para uso diário, não em efeitos.

## Estado atual

- Tema GTK e XFWM: [Nordic](https://github.com/EliverLara/Nordic)
- Ícones: [Tela Circle Nord Dark](https://github.com/vinceliuice/Tela-circle-icon-theme)
- Fonte da interface: Noto Sans 10
- Fonte do terminal: JetBrainsMono Nerd Font 10
- Terminal: Kitty com paleta Nord e transparência de 92%
- Shell: Zsh com badges pill Starship e eza com ícones
- Painel: único, superior, 28 px, `#2E3440` com 92% de opacidade
- Painel: Whisker Menu, lista de janelas, área de notificação, energia e relógio `%H:%M`
- Área de trabalho: sem ícones
- Janelas: Picom com cantos de 12 px e sombras discretas
- Wallpaper: escuro e compatível com Nord; a imagem é uma escolha local e não é versionada

## Dependências

```text
xfce4
xfce4-whiskermenu-plugin
xfce4-power-manager-plugins
fonts-noto-core
kitty
picom
starship
eza
git
```

`starship.toml` é a configuração completa e específica deste rice Nord. O XFWM continua como gerenciador de janelas, mas o compositor nativo fica desativado: o Picom é o único compositor. Não há blur, Conky, dock, Rofi, Polybar, animações ou CSS grande.

Consulte o [tutorial](TUTORIAL.md) para instalar e reproduzir a configuração.
