# MPV

MPV é um player de vídeo leve, aberto e altamente configurável. Nesta pasta, `mpv.conf` define reprodução, imagem, áudio e legendas; `input.conf` define atalhos extras.

Para usar esta configuração:

```bash
mkdir -p "$HOME/.config/mpv"
ln -s "$HOME/dotfiles/mpv/mpv.conf" "$HOME/.config/mpv/mpv.conf"
ln -s "$HOME/dotfiles/mpv/input.conf" "$HOME/.config/mpv/input.conf"
```

## Atalhos úteis

| Tecla | Ação |
| --- | --- |
| `Space` | Pausar ou retomar |
| `q` | Fechar o player |
| `f` | Alternar tela cheia |
| `←` / `→` | Voltar ou avançar 5 s |
| `Shift` + `←` / `→` | Voltar ou avançar 30 s |
| `↑` / `↓` | Aumentar ou diminuir volume |
| `m` | Silenciar |
| `a` | Trocar faixa de áudio |
| `s` | Trocar legenda |
| `Ctrl` + `+` / `-` | Aumentar ou diminuir legenda |
| `Alt` + `↑` / `↓` | Mover legenda verticalmente |
| `d` | Alternar debanding |
| `S` | Salvar screenshot em `~/Pictures/mpv/` |
| `.` / `,` | Avançar ou voltar um frame |
