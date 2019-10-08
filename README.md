# PhoneBook-Vue

Простая телефонная книга.

### Задание:

Необходимо сделать веб-страницу – телефонную книгу в виде таблицы с контактами.

Использовать:
- Фреймворк Vue.js,
- Система Vue CLI для разработки приложения. 

В каждой строке должен быть порядковый номер контакта, начиная с единицы, и должна быть кнопка для удаления клнтакта. По нажатию на нее строка должна удаляться. При этом номера строка перевычисляются.

- Форма для заполнения таблицы: 
  - рядом с таблицей сделать форму с полями Фамилия, Имя, Номер телефона и кнопкой для добавления строки.
  - По нажатию на кнопку, должна выполняться валидация, что все поля заполнены.
  - Незаполненные поля нужно выделить визуально (цветом границ или цветом фона). И нужно добавить на страницу сообщение, что необходимо заполнить поле «Имя» и т.д., смотря какие поля не заполнены.
  - Если валидация прошла успешно, то все поля очищаются, а в таблицу в конец добавляется новая строка с этими данными. При этом должны сброситься стили и сообщения валидации.

### Усложнения по задаче:
- Сделайте, чтобы по нажатию на кнопку удаления строки появлялось сообщение-confirmation. Библиотеку для этого выберите и подключите сами. Строка должна удаляться только если пользователь на это согласился
- Валидация, что контакт с таким номером уже добавлен. В этом случае выводить сообщение валидации, а строку в таблицу не добавлять.
- Сделать слева дополнительный столбец с чек-боксами для выбора строк.  При нажатии на кнопку удаления, удалять все выбранные строки.
- В столбце с чекбоксами в шапке сделать еще один чекбокс. Если его выбирают, то выбираются все строки таблицы. Если его убирают, то очищается выбор всех строк.
- Над таблицей сделать фильтр – текстовое поле, в которое пользователь может вводить текст. И рядом две кнопки - одна применяет фильтр, вторая сбрасывает. Фильтр ищет по всем полям, без учета регистра. Если фильтр сбросят, то должны показаться все данные.

### Сборка и запуск сервера
```
npm run serve
```

### Сборка и минификация для выкладки в production
```
npm run build
```
