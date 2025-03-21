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

16. Заходим в браузер и переходим по адресу <b> localhost:3000</b>

Вводим

<b>Логин:</b> admin

<b>Пароль:</b> admin

![image](https://github.com/user-attachments/assets/a13e7c00-1225-4d30-910c-714e50bfa832)

17. Попадаем на страницу <b>Home</b>

![image](https://github.com/user-attachments/assets/9639c08f-ecf0-41c7-a804-92f37276c9f7)

18. Заходим в конфигурационный файл докера с помощью команды `vi docker-compose.yaml`

![image](https://github.com/user-attachments/assets/def93501-3bc7-4d8e-aa6a-078f3b0ea08c)

19. Выходим вписав команду `:wq`

![image](https://github.com/user-attachments/assets/e8f57f3f-bd5e-43d5-93f6-06a3fe62ebe1)

20. Запускаем grafana с помощью  `sudo docker compose up -d`

![image](https://github.com/user-attachments/assets/96fac0e6-4f00-42b3-8d47-f10058fe6867)

21. Чтобы остановить grafana понадобится команда `sudo docker compose stop`

![image](https://github.com/user-attachments/assets/f4cc977a-9d1c-4dff-ae7a-a7298a536889)

22. А чтобы полностью остановить grafana понадобится команда `sudo docker compose down`

![image](https://github.com/user-attachments/assets/e96c1a50-34c0-469f-9c6c-bfd83fe61951)

# Prometheus

23. Скопировал конфигурационные файлы с github командой `sudo git clone https://github.com/Rusya6300/Install-GRAFANA.git`

![image](https://github.com/user-attachments/assets/60ebd695-ae16-4069-b8de-e517239d20e0)

24. Проверил, что репозиторий успешно установился командой `ls`

![image](https://github.com/user-attachments/assets/f4e50f71-3b3b-425f-a37c-1c84f023e679)

25. копируем конфигурационный файл докера используя команду `cp docker-compose.yaml /home/ruslan/`

![image](https://github.com/user-attachments/assets/24836b08-8e5a-41a4-9c0f-0c0a7851c7db)

Здесь у меня возникла проблема с копированием файла `prometheus.yaml` 

![image](https://github.com/user-attachments/assets/e54118b3-de49-48ae-902d-d4571e3a0e06)

И тогда я перешел в директорию где расположен файл и скопировал его оттуда 

![image](https://github.com/user-attachments/assets/ec02ccd8-b6f2-4273-93a1-6c92c6196ded)

Проверил, скопировались ли файлы командой `ls`

![image](https://github.com/user-attachments/assets/cb53c362-a9c0-4fc7-97f7-ab3b05ab87af)

26. Переносим конфигурационный файл prometheus.yaml в конфиг Grafana используя команду `mv prometheus.yaml /mnt/common_volume/swarm/grafana/config`

![image](https://github.com/user-attachments/assets/afcd4825-d8cc-4f8a-908e-8f79feb395c8)

27. Проверяем наличие файла командой `ls`

![image](https://github.com/user-attachments/assets/85f8da82-d7e1-45ac-aa42-d01bb93177d7)

28. Запускаем docker compose в фоном режиме командой `sudo docker compose up -d`

![image](https://github.com/user-attachments/assets/0d842259-9f02-4b9a-983b-4ee10b54ee42)

29. Переходим по адресу <b> localhost:3000</b>

![image](https://github.com/user-attachments/assets/98cb51a0-f8fd-451b-9a19-a59357faca58)


![image](https://github.com/user-attachments/assets/8a47906c-f20f-4571-9431-2a9eed1467e8)
