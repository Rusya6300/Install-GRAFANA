# LAB1_Установка Docker на Oracle Linux
1. Начал с установки пакета <b>wget</b>, используя команду `sudo yum install wget`, данный пакет даёт возможность загружать файлы из интернета

![image](https://github.com/user-attachments/assets/0a360e80-de3a-4ba4-ba61-820676431910)

2. Далее установил пакет <b>curl</b> с помощью команды ``sudo yum install curl``. Данный пакет даёт возможность отправлять HTTP/HTTPS запросы.

![image](https://github.com/user-attachments/assets/f6dbb177-d27d-4afc-93b4-fc0fdf355471)

3. Копирую репозиторий докера, для того чтобы его потом установить, используя <b>wget</b> используя тег <b>-P</b> для чтения <br>``sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo``

![image](https://github.com/user-attachments/assets/a22d9f73-91be-4fc3-9c71-58cbb08edcc5)

4. C помощью пакета yum устанавливаем докер из копированного репозитория выше
`sudo yum install docker-ce docker-ce-cli containerd.io`

![image](https://github.com/user-attachments/assets/fe8fa00e-0b2c-4f72-9061-daaeac6b7e2b)
![image](https://github.com/user-attachments/assets/68d29c58-f217-4839-8142-6dd5ecc819ee)

5. Запускаем докер используя команду `sudo systemctl enable docker --now` эта команда добавляет doker в список служб, которые запустятся при запуске ОС

>![image](https://github.com/user-attachments/assets/8d6f1d10-89e2-46f4-9a41-df90a3f55baf)

6. Получаем последнюю версию Docker Compose, используя команду `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

![image](https://github.com/user-attachments/assets/9bf8675c-442d-4bfc-9eab-53b40a37405a)

7. Скачиваем и устанавливаем последнюю версию Docker Compose с помощью команды `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose` 

![image](https://github.com/user-attachments/assets/79e40e16-9783-4cf3-9de3-ef2bf69280b5)

8. Устанавливаем права на выполнение (делает файл исполняемым) `sudo chmod +x /usr/bin/docker-compose` и проверяем установленную версию docker c помощью команды `docker --version`

![image](https://github.com/user-attachments/assets/d4d7bb88-d42d-46bc-a350-ebcb4f2c0ecc)

9. Клонируем репозиторий с github, где содержится Grafana с помощью команды `git clone https://github.com/skl256/grafana_stack_for_docker.git`

![image](https://github.com/user-attachments/assets/9872f907-9a25-40de-b9c0-9f7db0e1e02a)

10. Переходим в директорию в Grafana с помощью команды `cd grafana_stack_for_docker` и создаем директори с помощью команды `sudo mkdir -p /mnt/common_volume/swarm/grafana/config`

![image](https://github.com/user-attachments/assets/ee49d302-c202-4a89-9f77-b39019722589)

11. Изменяем владельца и группу для указанных директорий и всех их содержимых файлов с помощью `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

![image](https://github.com/user-attachments/assets/5e70a4e5-f74b-4c6c-a86f-08802eaaa55a)

12.Создаем файл конфигурации с помощью команды `touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

13. Копируем все файлы из директории <b>config</b> в <b>/mnt/common_volume/swarm/grafana/config/</b> c помощью команды `cp config/* /mnt/common_volume/swarm/grafana/config/`

14. Переименовываем файл <b>grafana.yaml</b> в <b>docker-compose.yaml</b> с помощью `mv grafana.yaml docker-compose.yaml`

![image](https://github.com/user-attachments/assets/9be473f4-f86e-423b-9a9c-c7f3d3ca3382)

15. Запускаем Docker Compose в фоновом режиме с помощью `sudo docker compose up -d`

![image](https://github.com/user-attachments/assets/34ae7c85-8e92-4a6e-a453-fe766bc3c08d)
