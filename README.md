Тестовое задание для кандидата на должность
HTML-верстальщик


Для задания используйте дизайн-макет в Figma:
https://www.figma.com/design/njB7vo9dIfM3PbXlZSOv9r/ЭКОЛОМ

1. Необходимо сверстать десктопную версию сайта, которая отображена на скрине. Верстать страницу целиком не требуется, адаптив не нужен.

2. Замерить время исполнения и указать его при сдаче задания. Время можно указать примерное (например, 6 часов).


Для правильной организации верстки в подобной ситуации, когда картинка выходит за рамки контентного контейнера и доходит до правой границы экрана (1920px), есть несколько подходов. Выбор зависит от того, как организован ваш макет и насколько такие эффекты будут повторяться.

### Вариант 1: Использовать два контейнера (один для контента, другой для полного экрана)
Этот подход часто используется в случаях, когда контент имеет фиксированную ширину, а некоторые элементы (например, картинки или фоны) должны растягиваться на всю ширину экрана.

- **Контент-контейнер** (1296px): Основная часть контента (текст, изображения, элементы интерфейса).
- **Контейнер на всю ширину экрана** (1920px или `100vw`): Блок для элементов, выходящих за рамки контентного контейнера (например, фоновая картинка).

#### Пример:
```html
<div class="full-width-container">
    <!-- Картинка или элемент, растянутый на всю ширину страницы -->
    <img src="image.jpg" alt="Картинка" class="full-width-image">
</div>

<div class="content-container">
    <!-- Основной контент, который находится в пределах 1296px -->
    <p>Здесь текст и другой контент, который находится в контейнере шириной 1296px.</p>
</div>
```

#### CSS:
```css
/* Контейнер для контента шириной 1296px */
.content-container {
    max-width: 1296px;
    margin: 0 auto; /* Центрируем контейнер */
    padding: 0 20px; /* Для отступов внутри */
}

/* Контейнер для элемента на всю ширину */
.full-width-container {
    width: 100vw; /* Полная ширина экрана */
    position: relative; /* Если нужно управлять позиционированием вложенных элементов */
}

/* Картинка, которая будет растягиваться на всю ширину */
.full-width-image {
    width: 100%; /* Занимает всю ширину контейнера */
    height: auto; /* Сохраняет пропорции */
}
```

### Вариант 2: Использовать `position: relative` и `position: absolute`
Если картинка выходит за рамки только одной стороны (например, вправо), и нет необходимости делать отдельный контейнер на 1920px, можно использовать позиционирование.

#### Пример:
```html
<div class="content-container">
    <!-- Обычный контент -->
    <p>Текст внутри контейнера шириной 1296px.</p>

    <!-- Картинка, которая выходит за границы контейнера -->
    <div class="image-container">
        <img src="image.jpg" alt="Картинка">
    </div>
</div>
```

#### CSS:
```css
/* Контейнер для контента */
.content-container {
    max-width: 1296px;
    margin: 0 auto;
    position: relative;
    padding: 0 20px;
}

/* Контейнер для картинки */
.image-container {
    position: relative;
    margin-right: -calc((1920px - 1296px) / 2); /* Выдвигаем вправо за пределы контейнера */
}

/* Картинка */
.image-container img {
    width: 100%;
    height: auto;
}
```

### Вариант 3: Верстать блок, отталкиваясь от размеров картинки
Этот вариант возможен, если картинка всегда будет иметь четкие размеры и не будет изменяться в зависимости от разрешения экрана. Однако, такой подход менее гибкий, так как жестко зашитые размеры могут повлиять на адаптивность.

#### Пример:
```css
.image-container img {
    width: 624px; /* Размер картинки по макету */
    position: relative;
    right: -300px; /* Выталкиваем картинку за пределы контейнера */
}
```

### Какой вариант выбрать?

- **Вариант 1** (с двумя контейнерами) — это более гибкий и предпочтительный подход, если такие элементы часто повторяются в макете и вам нужно обеспечить адаптивность.
- **Вариант 2** (с использованием `position: relative` и `absolute`) хорош для случаев, когда только один элемент выходит за рамки и вы хотите управлять его позиционированием относительно контента.
- **Вариант 3** лучше использовать в исключительных случаях, когда размеры картинки жестко заданы и нет необходимости в гибкости макета.

### Рекомендация:
Если у вас есть несколько блоков, в которых картинка или фон должны выходить за границы основного контейнера, лучше использовать **два контейнера**: один для контента (1296px), другой — для элементов, растянутых на всю ширину экрана (1920px или `100vw`).