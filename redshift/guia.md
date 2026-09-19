# Redshift

Redshift reduz a temperatura de cor da tela para um tom mais quente. Esta configuração mantém um filtro leve de **4400K** o dia inteiro: as temperaturas de dia e noite são iguais e não há transição.

## Instalação e configuração

```bash
sudo apt install redshift
mkdir -p "$HOME/.config/autostart"
ln -s "$HOME/dotfiles/redshift/redshift.conf" "$HOME/.config/redshift.conf"
ln -s "$HOME/dotfiles/redshift/Redshift.desktop" \
  "$HOME/.config/autostart/Redshift.desktop"
```

O autostart é exclusivo do XFCE e usa `randr`, apropriado para a sessão X11. Saia e entre novamente na sessão, ou inicie manualmente:

```bash
redshift -m randr
```

## Uso

| Comando | Ação |
| --- | --- |
| `redshift -m randr` | Ativa o filtro nesta sessão |
| `redshift -x` | Restaura as cores normais |
| `pkill redshift` | Encerra o Redshift |

Os valores `lat=0` e `lon=0` usam localização manual. Como `temp-day` e `temp-night` são iguais, o filtro permanece em 4400K enquanto o processo estiver ativo.
