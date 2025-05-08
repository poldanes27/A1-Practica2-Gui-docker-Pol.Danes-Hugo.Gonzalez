# Docker Ubuntu + LXDE + VNC + Python + SSH

Aquest contenidor ofereix un Ubuntu amb escriptori gràfic lleuger LXDE via VNC, amb suport per Python i connexió remota per SSH.

## 🔧 Requisits

- Docker
- Client VNC (Remmina)
- Port forwarding configurat a VirtualBox:
  - 5901 → VNC
  - 2222 → SSH

## 🚀 Instruccions

### Construir la imatge

```bash
docker build -t ubuntu-vnc-lite .
```

### Executar el contenidor

```bash
docker run -p 5901:5901 -p 2222:22 --rm ubuntu-vnc-lite
```

### Connexió VNC

1. Obre Remmina
2. Connexió a `localhost:5901`
3. Usuari: `developer`, contrasenya: `developer`

### Connexió SSH

```bash
ssh developer@localhost -p 2222
# contrasenya: developer
```

### Python

```bash
python3
```
