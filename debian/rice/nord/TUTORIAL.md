# Tutorial: Rice Nord no Debian 13 + XFCE + X11

Este guia reproduz o rice documentado aqui. Ele presume uma sessão XFCE em X11 e configura tudo no usuário atual.

## 1. Instale os pacotes

```bash
sudo apt update
sudo apt install -y \
  xfce4 \
  xfce4-whiskermenu-plugin \
  xfce4-power-manager-plugins \
  fonts-noto-core \
  kitty \
  picom \
  starship \
  rofi \
  eza \
  git
```

## 2. Salve a configuração atual

```bash
mkdir -p ~/backup-xfce-before-nord
cp -a ~/.config/xfce4 ~/backup-xfce-before-nord/
cp -a ~/.themes ~/backup-xfce-before-nord/ 2>/dev/null || true
cp -a ~/.local/share/icons ~/backup-xfce-before-nord/icons 2>/dev/null || true
cp -a ~/.config/rofi ~/backup-xfce-before-nord/ 2>/dev/null || true
```

## 3. Instale tema e ícones

```bash
mkdir -p ~/.themes ~/.local/share/icons
git clone --depth 1 https://github.com/EliverLara/Nordic.git /tmp/Nordic
cp -a /tmp/Nordic ~/.themes/Nordic

git clone --depth 1 https://github.com/vinceliuice/Tela-circle-icon-theme.git /tmp/Tela-circle
/tmp/Tela-circle/install.sh -c nord
```

Instale também a fonte usada pelo Kitty a partir deste repositório. Ajuste o caminho caso o clone esteja em outro local:

```bash
mkdir -p ~/.local/share/fonts
cp -a ~/dotfiles/fonts/JetBrainsMonoNerd ~/.local/share/fonts/
fc-cache -f
```

## 4. Aplique o XFCE

Execute os comandos dentro da sessão gráfica XFCE. Eles usam `xfconf-query`, já fornecido pelo XFCE.

```bash
xfconf-query -c xsettings -p /Net/ThemeName -s Nordic
xfconf-query -c xsettings -p /Net/IconThemeName -s Tela-circle-nord-dark
xfconf-query -c xsettings -p /Gtk/FontName -s 'Noto Sans 10'
xfconf-query -c xsettings -p /Gtk/MonospaceFontName -s 'JetBrains Mono 10'

xfconf-query -c xfwm4 -p /general/theme -s Nordic
xfconf-query -c xfwm4 -p /general/title_font -s 'Noto Sans Bold 10'

xfconf-query -c xfce4-desktop -p /desktop-icons/style -s 0
```

Configure um único painel superior, de 28 px, travado e sem ocultação. Deixe os itens nesta ordem:

```text
Whisker Menu · Window Buttons · Separator expansível · Notification Area · Power Manager · Clock
```

No painel, use cor sólida `#2E3440`, opacidade de 92% e relógio no formato `%H:%M`. Remova ou desative o painel inferior; não apague lançadores caso queira preservá-los para outro uso.

## 5. Configure o Kitty

Crie `~/.config/kitty/nord.conf`:

```conf
foreground #D8DEE9
background #2E3440
selection_foreground #2E3440
selection_background #88C0D0
cursor #88C0D0
cursor_text_color #2E3440
active_border_color #88C0D0
inactive_border_color #4C566A

color0 #3B4252
color1 #BF616A
color2 #A3BE8C
color3 #EBCB8B
color4 #81A1C1
color5 #B48EAD
color6 #88C0D0
color7 #E5E9F0
color8 #4C566A
color9 #BF616A
color10 #A3BE8C
color11 #EBCB8B
color12 #81A1C1
color13 #B48EAD
color14 #8FBCBB
color15 #ECEFF4
```

Adicione esta linha a `~/.config/kitty/kitty.conf`, preservando o restante do arquivo:

```conf
include nord.conf
```

Use `font_family JetBrainsMono Nerd Font` e `font_size 10.0`. Reabra o Kitty para carregar a paleta.

## 6. Configure o prompt e as listagens

Este rice possui uma configuração Starship própria em `starship.toml`. A partir desta pasta, instale-a assim:

```bash
mkdir -p ~/.config/dircolors
ln -sfn ~/dotfiles/debian/rice/nord/starship.toml ~/.config/starship.toml
ln -sfn ~/dotfiles/zsh/.config/dircolors/nord ~/.config/dircolors/nord
```

O link mantém as cores do `dircolors` sincronizadas com o arquivo versionado em `zsh/.config/dircolors/nord`.

No `~/.zshrc`, carregue o arquivo de cores antes das configurações de completion e o Starship depois delas:

```zsh
if [[ -f "$HOME/.config/dircolors/nord" ]]; then
  eval "$(dircolors -b "$HOME/.config/dircolors/nord")"
else
  eval "$(dircolors -b)"
fi

if command -v starship >/dev/null; then
  eval "$(starship init zsh)"
fi
```

O prompt mostra badges pill para diretório, Git e alterações Git, seguidos de `❯`. O `dircolors` deixa diretórios azuis, links ciano, executáveis verdes e erros vermelhos.

Para listagens com ícones e diretórios primeiro, adicione ao `~/.zshrc`:

```zsh
if command -v eza >/dev/null; then
  alias ls='eza --icons --group-directories-first --oneline'
  alias ll='eza --icons --group-directories-first --long --header --git'
  alias la='eza --icons --group-directories-first --all --long --header --git'
  alias lt='eza --icons --group-directories-first --tree --level=2'
fi
```

Use `ls` para uma lista vertical com ícones, `ll` para detalhes, `la` para incluir ocultos e `lt` para uma árvore de até dois níveis. Abra um novo Zsh com `exec zsh`.

## 7. Configure cantos arredondados com Picom

Crie `~/.config/picom/picom.conf`:

```conf
backend = "xrender";
corner-radius = 12;

shadow = true;
shadow-radius = 10;
shadow-opacity = 0.22;
shadow-offset-x = -5;
shadow-offset-y = -5;

rules = (
  { match = "window_type = 'dock'"; corner-radius = 0; shadow = false; },
  { match = "window_type = 'desktop'"; corner-radius = 0; shadow = false; },
  { match = "fullscreen"; corner-radius = 0; shadow = false; },
);
```

Desative o compositor nativo e inicie o Picom:

```bash
xfconf-query -c xfwm4 -p /general/use_compositing -s false
picom --daemon --config ~/.config/picom/picom.conf
```

Para iniciar em cada login, crie `~/.config/autostart/picom.desktop`. Substitua `SEU_USUARIO` pelo nome da sua conta:

```ini
[Desktop Entry]
Type=Application
Name=Picom
Exec=picom --config /home/SEU_USUARIO/.config/picom/picom.conf
OnlyShowIn=XFCE;
X-GNOME-Autostart-enabled=true
```

## 8. Configure o Rofi

A configuração versionada usa a paleta Nord, JetBrainsMono Nerd Font, ícones, busca fuzzy e uma lista de sete resultados. Instale-a a partir do clone deste repositório:

```bash
mkdir -p ~/.config/rofi
ln -sfn ~/dotfiles/debian/rice/nord/rofi/config.rasi \
  ~/.config/rofi/config.rasi
```

Na sessão gráfica XFCE, configure `Super+Space` para abrir o launcher de aplicativos:

```bash
xfconf-query -c xfce4-keyboard-shortcuts \
  -p '/commands/custom/<Super>space' \
  -n -t string -s 'rofi -show drun'
```

Teste a configuração e confira o atalho registrado:

```bash
rofi -show drun
xfconf-query -c xfce4-keyboard-shortcuts \
  -p '/commands/custom/<Super>space'
```

O primeiro comando abre o launcher; `Esc` o fecha. O segundo deve exibir `rofi -show drun`.

## 9. Finalize

Escolha um wallpaper escuro com tons Nord e saia/entre na sessão. Verifique o compositor com `pgrep -a picom`; deve haver apenas um processo Picom.
