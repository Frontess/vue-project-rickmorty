# Rick and Morty Characters App

Этот проект представляет собой веб-приложение, которое отображает персонажей из популярного анимационного сериала “Rick and Morty”.  
Оно использует Vue.js для создания интерактивного интерфейса для просмотра и фильтрации персонажей.

<img width="1321" alt="Снимок экрана 2024-05-30 в 14 53 17" src="https://github.com/Frontess/vue-project-rickmorty/assets/127450758/093fc44b-f466-48f9-9cc6-14728dcafae1">

## Особенности проекта

1. Карточки персонажей:
- Персонажи отображаются в виде карточек, аналогично дизайну из предоставленного источника API.
- Вместо ссылок на карточках используется текст.

2. Пагинация:
- Реализована пагинация с использованием API.
- Пользователи могут переходить на разные страницы с данными о персонажах.

3. Фильтрация:
- Реализована фильтрация по полям “name” и “status” с использованием API.
- Пользователи могут применять фильтры, нажимая кнопку “Применить”.

4. Стилизация:
- Для элементов пагинации и фильтрации используются стандартные HTML-теги (input, select).

## Структура проекта
Проект состоит из следующих компонентов:

- Input: Обрабатывает ввод пользователя для фильтрации персонажей.
- Characters: Отображает карточки персонажей и применяет пагинацию и фильтрацию.
- Pagination: Предоставляет элементы управления для переключения страниц.

## Используемые технологии
- Vue.js
- Axios (для запросов к API)

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
