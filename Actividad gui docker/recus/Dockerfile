# Utiliza la imagen oficial de Ubuntu 24.04 como base
FROM ubuntu:24.04

# Evita interacciones durante instalaciones (como selección de zonas horarias)
ENV DEBIAN_FRONTEND=noninteractive

# Actualiza paquetes e instala XFCE, VNC y herramientas esenciales
RUN apt update && apt install -y \
    xfce4 xfce4-goodies tightvncserver \       # Entorno de escritorio XFCE y servidor VNC
    wget curl openssh-server python3 python3-pip \  # Utilidades básicas y servidor SSH
    dbus-x11 x11-xserver-utils sudo nano git software-properties-common \ # Soporte gráfico, sudo, editores y git
    && apt clean  # Limpia caché de APT para reducir tamaño de la imagen

# Crea un usuario llamado 'docker' con su directorio home y le da permisos sudo
RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

# Permite que el usuario 'docker' use sudo sin tener que introducir contraseña
RUN echo "docker ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Prepara los directorios necesarios para el servidor SSH
RUN mkdir -p /etc/ssh /var/run/sshd

# Instala Visual Studio Code desde el repositorio oficial de Microsoft
RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg \
    && install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/ \                      # Añade la clave GPG del repositorio
    && sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list' \  # Añade el repo
    && apt update && apt install -y code \   # Instala VS Code
    && rm microsoft.gpg                     # Borra el archivo de clave ya copiado

# Configura el entorno del usuario 'docker' para que funcione VNC correctamente
RUN mkdir -p /home/docker/.vnc                                 # Crea la carpeta .vnc donde se guardan config y scripts
COPY scripts/startup.sh /home/docker/.vnc/xstartup             # Copia el script que arranca XFCE al conectarse por VNC
RUN chmod +x /home/docker/.vnc/xstartup                        # Da permisos de ejecución al script
RUN chown -R docker:docker /home/docker/.vnc                   # Establece el propietario correcto de los archivos

# Cambia el contexto al usuario 'docker' para las siguientes instrucciones
USER docker

# Configura la contraseña del servidor VNC (en este caso 'docker') en formato cifrado
RUN echo "docker" | vncpasswd -f > /home/docker/.vnc/passwd
