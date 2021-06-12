---
title: Индивидуальный проект <Этап 1>
summary: Создать шаблон, изменить аватар владельца и добавить описание
tags:
- Personal project
date: "2021-05-01T00:00:00Z"

# Optional external URL for project (replaces project detail page).
#external_link: ""

#image:
#  caption: Photo by rawpixel on Unsplash
#  focal_point: Smart

#links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
#url_code: ""
#url_pdf: ""
#url_slides: ""
#url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: content/slides
---


## Задание

- Размещение на Github заготовки для персонального сайта
- Установка фотографии владельца сайта
- Установка описания владельца сайта

## Выполнение

### Размещение сайта на github

1. Организация рабочего пространства (команда mkdir). (рис.2.1 и рис.2.2)

![создание каталогов](pics/1.png){ #fig1:1 width=100% }

![создание каталогов(продолжение)](pics/2.png){ #fig1:1 width=100% }

2. Создаем директорию blog (mkdir), переходим в нее (cd) и скачиваем туда шаблон нашего будущего сайта (git clone). (рис.2.3)

![скачивание шаблона](pics/3.png){ #fig1:1 width=100% }

3. Запускаем hugo (hugo). (рис.2.4)

![скачивание шаблона](pics/4.png){ #fig1:1 width=100% }

4. Удаляем ненужные файлы (rm). (рис.2.5)

![удаление файлов из шаблона](pics/5.png){ #fig1:1 width=100% }

5. Инициализируем git (git init), коммитим (git add . и git commit). (рис.2.6)

![работа с git](pics/6.png){ #fig1:1 width=100% }

6. Создаем репизитории н для сайта на github. (рис.2.7)

![список репозиторий на github](pics/7.png){ #fig1:1 width=100% }

7. Выкладываем репозиторий на github (remote add origin, push). (рис.2.8)

![выкладывание репозитория на Github](pics/8.png){ #fig1:1 width=100% }

8. Создание подмодуля (git submodule add). (рис.2.9)

![создание подмодуля](pics/a.png){ #fig1:1 width=100% }

9. Добавляем все в локальный репозиторий git и отправляем его в удаленный репозиторий на GitHub. (рис.2.10)

![выкладка данных в удаленный репозиторий](pics/b.png){ #fig1:1 width=100% }

10. Обновляем HTML через hugo (hugo, git add, git commit). (рис.2.11)

![выкладывание репозитория на Github](pics/9.png){ #fig1:1 width=100% }

11. Выкладываем все на github(git push). (рис.2.11)

![выкладывание репозитория на Github](pics/10.png){ #fig1:1 width=100% }

### Смена аватара владельца

Заменяем картирнку avatar.jpg на нашу с таким же наименованием в папке .../blog/git/content/authors.

### Изменение информации о пользователе

1. В папке .../blog/git/content/authors открываем файл _index.md и редактируем его.

![редактирование _index.md](pics/14.png){ #fig1:1 width=100% }

2. Обновляем наш сайт через hugo и github (hugo, git add, git commit).

![запускаем hugo](pics/15.png){ #fig1:1 width=100% }

![обновляем данные](pics/16.png){ #fig1:1 width=100% }

## Результат

![мой сайт-визитка](pics/18.png){ #fig1:1 width=100% }
