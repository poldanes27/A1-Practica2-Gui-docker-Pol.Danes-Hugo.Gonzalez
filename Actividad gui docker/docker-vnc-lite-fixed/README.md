# Docker Ubuntu

## Requisits

- Docker
- Client VNC
- Port forwarding configurat a VirtualBox:
  - 5901 → VNC
  - 2222 → SSH

## Instruccions

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
