# <a name="up" /> Портфолио тестировщика 
Здесь собраны проекты, которые я тестировала после самостоятельного обучения на тестировщика.
1. Приложение Zonatelecom (версия 3.0.6)
2. Сайт компании Dilsys (2023 г.) 


## <a name="test-design" />Проектирование тестов приложения Zonatelecom

```diff
- Понимание требований (пользовательский сценарий)
- Определение цели (что будет проверяться сценарием)
- Описание шагов (написание сценария) | Блок-схема | Классы эквивалентности |Чек-кейсы и чек-лист| Тест-анализ 
- Документация
```


### Задание 1

**1. Визуализация требований**

Проанализировать требования к мобильному приложению Zonatelecom и нарисовать mindmap.
![Mindmap](https://i.ibb.co/mF5vKPx/Zonatelecom.png) 

[Карта в большом разрешении](https://i.ibb.co/mF5vKPx/Zonatelecom.png)

**2. Требования**:
   Авторизация пользователя для последующего использования приложения.

**3. Цели**:
   Сценарием будет проверяться возможность авторизации с помощью кода и звонка.

**4. Тестовый сценарий**:
   Сценарий для ручного тестирования авторизации в пользовательском интерфейсе. 

USE CASE на авторизацию:
Предусловие:
1. Пользователь запустил приложение и перед ним окно с полем для ввода номера телефона.

Сценарий:
1. Выбрать страну номера телефона
   
3. Ввести номер телефона
   
5. Нажать далее
   
4. (а) Для авторизации по SMS: нажать кнопку "вход по SMS"

4. (а)  Для авторизации по звонку: нажать кнопку "вход по вашему звонку"

5. (а) Для авторизации по SMS: нажать кнопку "отправить код"

5. (а)  Для авторизации по звонку: нажать кнопку "позвонить"

6. (а) В появившемся окне нажать кнопку "разрешить" и дождаться кода/звонка для автоматической авторизации

7. При выборе звонка авторизация происходит автоматически.

Негативные кейсы:
- На этапе разрешения приложению прочитать сообщение и ввести код нажата кнопка "Отклонить"
- Номер телефона введён неправильно без отправки SMS-кода/звонка
- Номер телефона введён неправильно и отправлен SMS-код/звонок



**5. Визуализация авторизации с помощью блок-схемы**

![block_diagram](https://i.ibb.co/Z266mgw/blockk.jpg)

**6. Составление тест-кейсов по сценарию**

Успешная авторизация.
![auto](https://i.ibb.co/KL6CtcW/11.jpg)

Авторизация с ошибками.
![auto22](https://i.ibb.co/r2YMW0K/auto22.jpg)

Написать тест-кейс на основе тестовых значений:

Правильный номер телефона - +79991115893

Неправильный номер телефона - +79115118676 



|Номер телефона|Разрешение|Авторизация код|Авторизация звонок|Возвращение в главное меню|Возможность менять тип авторизации|
|:--------------|:---------|:------|:-------------------|:------------------|:------------------|
|+79991115893        |да  |   да   |     да                  | да     |да     |
|           |нет  |  нет    |   нет       | да|    да     |
|+79115118676            |да  |  нет    |   нет       | да|    да     |
|           |нет  |  нет    |   нет       | да|    да     |

   Фактически тестами покрыта только часть основной функциональности – авторизация с помощью ввода правильном и ошибочного номера. Также подготовлены данные для составления тест-кейсов, проверяющих возможность авторизации при изменении параметров.

   Осталось подготовить данные и написать тест-кейсы для тестирования ввода имени и даты в окне добавления календаря.

**7. Создание чек-листа**

1)Авторизоваться через российский номер телефона

2)Авторизоваться через украинский номер телефона

3)Авторизоваться одновременно на сайте и приложении телефона


### Задание 2
Составить классы эквивалентности для ввода имени и даты.

**1. Классы эквивалентности**
<details>
<summary>Поля имени</summary>

***

Длина поля - от 0 до 20 символов.


|Название класса|Тип класса|Границы|Тестовые данные внутри класса|Тестовые данные на границах|
|:--------------|:---------|:------|:------------------------------|:------------------------|
|от 1 до 20 символов        |диапазон  | 1, 20     |    Иванов Иван Иванович   | 1 символ: "И"|
|       |  |     |      | 2 символа: "Ив"|
|       |  |     |      | 19 символов: "Александр-Фердинанд"|
|       |  |     |      | 20 символов: "Иванов Иван Иванович"|
|       |  |     |      | 21 символов: "Гитинамагомедгаджияв"|
|от -∞ до 0|диапазон  | 0 |         | (не даёт ввести)	|
|от 21 до +∞| диапазон | 21 | Анастасия | (не даёт  ввести)


Вводимые значения:

|Название класса|Тип класса|Границы|Тестовые данные внутри класса|
|:--------------|:---------|:------|:-------------------|
|Строка, содержащая русские буквы |набор  | Корректный  | "Анастасия"|    
|Строка, содержащая цифры |набор  | Корректный  | "Анастасия3"|
|Строка, содержащая пробел в середине текста|набор  | Корректный  | "Анаста сия"|
|Строка, содержащая пробел в начале текста | набор  | Корректный  | " Анастасия"|
|Строка, содержащая пробел в конце текста |набор  | Корректный  | "Анастасия  "|
|Строка, содержащая запятую |набор  | Корректный  | "Анаста,сия"|
|Строка, содержащая тире |набор  | Корректный  | "Анаста-сия"|
|Строка, содержащая точку |набор  | Корректный  | "Анастасия."|
|Строка, содержащая латинские буквы |набор  | Корректный  | "Anastasia"|
|Строка, содержащая символы других языков |набор  | Корректный  | "अ"|
|Строка, содержащая спецсимволы |набор  | Корректный  | "%;$#?&*!"|
|Строка с двойным именем |набор  | Корректный  | "Ева-Мария"|
Строка с именем больше 20 |набор  | Некорректный  | "Гитинамагомедгаджияв"|

</details>


<details>
<summary>Поля даты начала заключения и даты освобождения</summary>


Тип поля: дата


|Название класса|Тип класса|Границы|Тестовые данные внутри класса|Тестовые данные на границах|
|:--------------|:---------|:------|:------------------------------|:------------------------|
|Минимальная и максимальная дата     |диапазон  | 01.01.2000 и 31.12.2060     | минимальная +1 и максимальная +1    |  01.01.2000 и 31.12.2060|
|Текущая дата и минимальная | диапозон | 15.12.2023 и 31.12.2060    | текущая -1 и +1 и минимальная -1     | 15.12.2023 и 30.12.2060|
|Дата окончания раньше даты начала| диапазон | 31.12.2060 и 01.01.2000   |      | 16.02.2005 и 12.10.2002|
|Случайная дата с условием (дата начала раньше даты окончания)| диапазон |13.05.2021 и 19.12.2029  |      | 20.07.2021 и 22.12.2030|



Вводимые значения:

|Название класса|Тип класса|Результат|Тестовые данные внутри класса|
|:--------------|:---------|:------|:-------------------|
|Минимум и максимум |набор  | Корректный  | 01.01.2000 и 31.12.2060|    
|Максимум и минимум|набор  | Некорректный | 31.12.2060 и 15.12.2023|
|Минимальная дата +5 и максимальная дата|набор  | Корректный  | 06.01.2023 и 31.12.2060|
|Минимальная дата и максимальная дата -5 |набор  | Корректный  | 01.01.2000 и 26.12.2026|
|Минимальная дата +1 и максимальная дата -1 |набор  | Корректный  | 02.01.2000 и 30.12.2026|
|Минимальная дата +1 и максимальная дата  |набор  | Корректный  | 02.01.2000 и 30.12.2026|
|Минимальная дата  и максимальная дата -1 |набор  | Корректный  | 01.01.2000 и 30.12.2026|
|Текущая дата начала и завтра конец |набор  | Корректный  | 15.12.2023 и 16.12.2023|
|Текущая дата конец -1 и завтра начало |набор  | Некорректный  | 14.12.2023 и 16.12.2023|
|Текущая дата конец  и текущая дата конец |набор  | Некорректный  | 15.12.2023 и 15.12.2023|
|Завтрашняя дата начало и текущая дата конец |набор  | Некорректный  | 16.12.2023 и 15.12.2023|



   Для класса "Дата освобождения раньше даты начала" за границу я брала данные отталкиваясь от даты составления тест-кейса - 15.12.2023. 
   То есть пыталась назначить дату заключения 16.12.2023, а дату освобождения 15.12.2023.
   Таким образом, мне удалось составить данные и провести тест по проверке ввода набора имени и даты освобождения и заключения с целью добавления календаря на главный экран приложения.

</details>

**2. Тест-анализ**

   Провести тест-анализ и составить тест-кейс для проверки позитивных значений ввода ФИО и даты.

|ФИО|Дата|
|:--------------|:---------|
|1. Мужское |Минимальная и максимальная дата |   
|2. Женское|Дата в 10 лет|
|3. Унисекс|Дата в 50 лет| 
|4. Редкое |Дата в 2 месяца|
|5. Длинное|Дата в 2 месяца|
|6. Короткое |Дата в 2 месяца|

   В данном тесте были объединены самые популярные значения и в таком случае уменьшено количество потенциальных проверок. 

### Задание 3

**Документация приложения**
1) FAQ
   - В приложении: в главном меню нажать на кнопку "Еще" с тремя точками, выбрать "Вопросы и ответы". ИЛИ В главном меню сверху нажать на кружок с вопросительным знаком. 
   - На сайте: https://www.zonatelecom.ru/support/faq
2) Лицензии 
   - Зайти на сайт, нажать "О компании", выбрать "Лицензии", откроется список лицензий.
3) Online-help
   - В приложении: в главном меню нажать на кнопку "Еще" с тремя точками, выбрать "Поддержка". Откроется окно для заказа звонка. После нажатия кнопки "Заказать" должно высветиться 'звонок успешно заказан'.
   - На сайте: Зайти на сайт, долистать до конца, найти кнопку "Обратный звонок от Зонателеком", в появившемся окне ввести свои данные "Имя" и "Мобильный телефон", затем выбрать через какое время позвонить и нажать "Обратный звонок".
4) Видео-инструкция по установке приложения.
   - Зайти на youtube, в поисковой строке ввести "Мобильное приложение Zonatelecom", открыть видео с канала ZTK. (Убедиться в правильности видео можно по аватарке Zonatelecom - зелёный и фиолетовый скреплённые квадраты).
   Таким образом, мне удалось ограничиться четырьми пунктами документации приложения поскольку тестирование проводится при самостоятельном обучении.
   


## <a name="test-design" />Проектирование тестов сайта Dilsys

```diff
- Понимание требований (пользовательский сценарий)
- Определение цели (что будет проверяться сценарием)
- Функциональное тестирование(ссылки, тестирование форм, тест-кейсы)
- Тестирование GUI (наличие грамматических и орфографических ошибок, локализация, масштабируемость, back button, влияние AdBlock)
```

### Задание 1

**1. Требования**:
   Информационный сайт компании, возможность заполнить и отправить форму для обратной связи.

**2. Цели**:
   Проверка форм на наличие ошибок. Функциональное и GUI - тестирование.

   Чек-лист: заказ товара через главное меню по каталогу.

Чек-кейс:

-    Открыть сайт: https://dilsys.com/.
-    В правой левой углу сверху нажать на три полоски.
-    На вкладке каталог выбрать "Накладные".
-    Навести курсов на товар "CUBE-130".
-    Нажать на товар "CUBE-130".
-    Рядом с товаром справа нажать кнопку "Заказать"
-    Заполнить формы стандартными данными Имя: Андрей; Телефон: +79517394332; E-mail: andrey@proton.me; Сообщение: заказ. Кроме этого будет автоматически указан товар "CUBE-130".
-    Нажать "Отправить заявку".
  
*Ожидания*

-    Открывается главная страница сайта.
-    В этой же вкладке появляется окно с тремяти таблицами "Компания", "Каталог" и "Проекты".
-    Открывается окно с товарами из каталога "Накладные" и слева в столбце строка "Накладные" выделена.
-    Товар должен выделяться прямоугольной рамкой.
-    Откроется новой окно с товаром "CUBE-130".
-    Справа появляется панель для заполнения формы.
-    Форма заполнена, выбранный товар CUBE-130 автоматически заполнен в форме "Продукт".
-    Заявка успешно отправлена. 
  
  
  ### Задание 2
  
   Чек-кейс на ввод формы "Имя". Мною была составлена таблица с позитивными тестами для уменьшения общего количества тестов, а также я попробовала в поле вводить различные негативные (по-моему мнению) варианты заполнения. 

![negativelist](https://i.ibb.co/Sm4Lh1x/image.jpg)

   Таким образом, после тестирования формы Имя мною были обнаружены возможности заполнения поля исключительно цифрами и даже с одновременно разным регистром. В таком случае, стоит спрашивать сценарий  у менеджера, как задумывали, что на выходе ожидается, а потом уже составлять баг-отчёты по документации. В данном же случае я лишь хочу от себя добавить, что при возможности ограничила бы ввод заполнения имени по нескольким условиям и затем уже тестировала граничные значения, классы эквивалентности.

   ### Задание 3 
  
   Проверка наличия грамматических и орфографических ошибок. Для этого я использовала расширение Spell Checker for Chrome.
   
![spell](https://i.ibb.co/M1Rhwfb/spell.png)

   В данном примере ошибок не найдено. Так же ещё попробовала перевести страницу на английский язык.

![eng](https://i.ibb.co/4TxBCdH/english.png)

   Перевод выполнялся автоматически через браузер Brave. Ошибок мною замечено не было.

   ### Задание 4

   Проверка отображения главной страницы на мобильной устройстве. Данный тест выполнялся  на устройстве Redmi 9. 

![mas](https://i.ibb.co/4P4DJ0r/mas3.png).

   Вывод: сайт отображается корректно. Изображения и текст иду последовательно. Есть возможность увеличивать и уменьшать отображение.
   
   ### Задание 5
   
   Проверка кнопки back button. Часто на этом бывают ошибки и поэтому я решила проверить будет ли что-то на сайте Dilsys.
   Вывод: при переходе на различные кнопки и открытие окон возвращение назад происходит корректно, возвращая на ту часть страницы, где пользовать был До выполнения следующего действия.

   ### Задание 6
   
   Работа сайта при наличии расширений в браузере. В 3-м задании я пользовалась расширением "Spell Checker for Chrome" и мною не ыбло обнаружено никаких неполадок. Попробую выполнять действия при включенном AdBlock. 
   Вывод: сам работает без изменений. 

   В общем и целом, после проведения небольшого 'беглого' тестирования некоторых элементов сайта я пришла в выводу о том, что несмотря на просту и лёгкость заполнения данных для обратной связи на сайте есть много недочётов. 
   Перечислю:
   1) При прокрутке главной страницы до низа кнопка "Телеграм" (с возможной ссылкой) - не работает.
   2) Имя при заполнении анкеты можно ввести почти любое.
   3) Невозможность учитывать сразу несколько фильтров при выборе товара.
   4) Дополнительное окно для связи отображается криво (ниже приложу скрин).

![forma]( https://i.ibb.co/cLtXPT3/forma.png).

   5) В разделе новости "Список элементов пуст".
   6) Если с главной страницы зайти в раздел "Проекты" и попробовать отсортировать проеты по одному из предлагаемых вариантов - ничего не произойдёт. Скрин приложу также ниже:
      
![project](https://i.ibb.co/Wp6qSRD/project.png).

   **Вывод:** Поскольку я не имею при себе документации и требований к сайту, то однозначно не могу сказать что устраивает пользователей и заказчиков, а что нет. Мною было найдено как минимум 6 спорных вопросов на которые я бы несомненно обратила внимание, сообщив информацию менеджеру или напрямую разработчику. 
    
[Наверх](#up)
