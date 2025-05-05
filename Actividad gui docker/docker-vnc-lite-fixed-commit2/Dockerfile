FROM dorowu/ubuntu-desktop-lxde-vnc

ENV DEBIAN_FRONTEND=noninteractive

# Desactivar repo de Chrome per evitar error GPG
RUN rm /etc/apt/sources.list.d/google-chrome.list || true

# Instal·la Python i SSH
RUN apt update && apt install -y python3 python3-pip openssh-server

# Crear usuari per SSH i configurar
RUN useradd -m developer && echo "developer:developer" | chpasswd

# Activar servei SSH
RUN mkdir /var/run/sshd

# Exposar ports VNC i SSH
EXPOSE 5901 22

# Inici del contenidor
CMD service ssh start && tail -f /dev/null
