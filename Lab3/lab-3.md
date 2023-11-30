# Задание 3

## Наша задача - cделать, чтобы после пуша в ваш репозиторий автоматически собирался докер образ и результат его сборки сохранялся куда-нибудь

Создадим репозиторий на github и загрузим на него необходимые файлы. Создадим в папке директорию .github/workflows.

[Ссылка на репозиторий](https://github.com/Giktg/Repo_for_cloud_lab3)

![Alt text](image-1.png)

Настроим workflow. Для этого создадим файл docker-build.yml внутри workflows. Конечный код:

```
name: Docker Build

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Build Docker image
      run: docker build -t docker-image:latest .

    - name: Save Docker image as tar
      run: docker save -o docker-image.tar docker-image:latest

    - name: Upload Docker image
      uses: actions/upload-artifact@v2
      with:
        name: docker-image
        path: docker-image.tar
```

# Проверка

Делаем пуш. Теперь зайдем в наш репозиторий на GitHub и откроем раздел Actions. В нем можно увидеть, что появился workflow.

![Alt text](image.png)

Как мы видим процесс успешно завершился

![Alt text](image-2.png)

Проверяем сработавший workflow и видим что наш образ забилдился и лежит в артефактах

![Alt text](image-3.png)

# Вывод

С помощью github actions мы настроили автоматическую сборку и выгрузку docker образа
