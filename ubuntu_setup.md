# 업데이트
sudo apt update && sudo apt upgrade -y


# 도커 설치
curl -fsSL https://get.docker.com | sudo sh

sudo usermod -aG docker $USER
newgrp docker

sudo systemctl enable --now docker

docker --version
docker compose version