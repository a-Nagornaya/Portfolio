<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>
<h1>Портфолио тестировщика</h1>
<p>В портфолио собраны учебные и тренировочные проекты, выполненные во время обучения.</p>
<a href="#designing-test"><h2>Проектирование тестов</h2></a>
<p> Тест-анализ | Ассоциативные карты | Блок-схемы
Тест-дизайн | Классы эквивалентности | Граничные значения
Тестовая документация | Чек-листы | Тест-кейсы</p>

<h2>Тестирование веб-приложений</h2>
<p>  Пользовательский интерфейс | Формы | DevTools | 
        Таблицы принятия решений | Баг-репорты</p>
<h2>Тестирование API</h2>
<p>  REST API | Postman</p>
<h2>Основы автоматизации тестирования</h2>
<p>JavaScript |</p>
</body>
</html>



        
<h3 name="designing-test">Задание 1 "Проектирование тестов"</h3>
<p>
<strong>1. Визуализируй требования</strong>
<br>Проанализируй требования к сервису Яндекс.Метро и нарисуй mindmap.<br>
<strong>2. Выдели классы эквивалентности и граничные значения</strong><br>
Проверь: «Откуда», «Куда».
Выдели объекты тестирования.
Определи классы эквивалентности. Укажи тип ограничений: диапазон или набор значений.
Определи граничные значения каждого класса, если применимо.
Выбери тестовые значения, которые проверят каждый класс; и границы, если они есть.
Не забудь проверить негативные сценарии.
</p> <br>
Решение:<br>
<details open>
<summary>Я подробно изучила описание сервиса и требования к Яндекс.Метро (привожу их ниже)</summary><br>

Яндекс Метро — сервис, который позволяет ориентироваться в метро с помощью мобильного устройства. В приложении есть схема метро, которая помогает построить маршрут и оценить время в пути. В нём также появляются актуальные уведомления о работе станций метро и изменениях графика работы.

Интерфейс:<br>
В интерфейсе есть две функциональные области: карта метро, область ввода станций метро. Карта двумерная. Можно перемещать свайпом. Масштабируется пинчем и спредом.<br>
Описание работы интерфейса: <br>
Если геолокация устройства пользователя определяется в городе с метро, то активной отмечена станция «Откуда», ближе к которой находится устройство. Если геолокация выключена, то поля «Откуда» и «Куда» пустые. Так же на стартовом экране есть кнопка «Настройка», в ней пользователь может выбрать город, язык и тему, а также очистить историю поиска, узнать версию приложения и оставить обратную связь. Город: в текущей версии команда проработала схемы метро для 36 городов. Язык: в текущей версии пользователь может выбрать один из двух языков: русский или английский. Тема: пользователь может выбрать тёмную или светлую тему. Если выставлен режим «Автоматически», то тема меняется автоматически: со светлой на тёмную в 18:00, с тёмной на светлую в 6:00. Время московское. Очистить историю поиска: пользователь может очистить историю поиска и маршрутов, нажав кнопку «Очистить историю поиска». Откроется всплывающее окно с подтверждением удаления. При нажатии кнопки «Удалить» история поиска и маршрутов удаляется. О приложении: пользователь может посмотреть версию сборки приложения и дополнительную информацию. Обратная связь: пользователь может оставить обратную связь. При нажатии на кнопку «Обратная связь» происходит переход в окно службы поддержки с помощью Webview. 
<br>
Логика работы полей «Откуда» и «Куда»:<br>
Если поля станций заполнены корректно, на карте отображаются точки А и В. Если поле «Откуда» заполнено некорректно, точка А не отображается. Если поле «Куда» заполнено некорректно, точка В не отображается. При некорректном значении поле очищается автоматически. Маршрут построится, только если заполнить поля «Откуда» и «Куда». Маршруты на карте интерактивные — пользователь может выбирать тапом станции. Пользователь может поменять местами названия станций в полях с помощью кнопки со стрелочками. Если одно поле пустое, то при нажатии кнопки название станции перемещается между полями. 
<br> Требование к вводимым символам:<br>	
Только буквы русского алфавита, цифры, пробел, тире. Длина не менее 1 и не более 50 символов. Пробелы до и после адреса исчезают при снятии фокуса. Если пользователь соблюдает правила ввода и под введённые символы попадает название станции, то оно отображается для выбора. Если правила не соблюдаются или станций, соответствующих введённым символам, не обнаружилось, станция не отображается.
</details>

<br>Ассоциативная карта
<img src="C:/Users/huawei/Downloads/drawing.svg" alt="Ассоциативная карта">

2. Классы эквивалентности и граничные значения
Поля ввода адреса (Откуда, Куда)
Длина поля
Название класса	Тип класса	Границы	Тестовые данные внутри класса	Тестовые данные на границах
от 1 до 50 символов	диапазон	1, 50	22 символов: "Преображенская площадь" 	1 символ: "П"
				49 символов: «Преображенская площадь Сокольническая линия красн»
				50 символов: " Преображенская площадь, Сокольническая линия красн"
от -∞ до 0	диапазон	0		0 символов: пустая строка
от 51 до +∞	диапазон	51	85 символов: " Преображенская площадь, Сокольническая линия, красная ветка московского метрополитена "	51 символ: " Преображенская площадь, Сокольническая линия красна "







Обязательность заполнения
Название класса	Тип класса	Границы	Тестовые данные внутри класса	Тестовые данные на границах
Поле заполнено	набор			"Преображенская площадь" 
Поле пустое	набор			Пустая строка


Вводимые значения
Название класса	Тип класса	Границы	Тестовые данные внутри класса
Строка, содержащая русские буквы	набор	Корректный	"Сокол" 
Строка, содержащая цифры	набор	Некорректный	"Преображенская площадь11" 
Строка, содержащая пробел в середине текста	набор	Корректный	"Преображенская площадь" 
Строка, содержащая пробел в начале текста	набор	Корректный	" Преображенская площадь"
Строка, содержащая пробел в конце текста	набор	Корректный	"Преображенская площадь "
Строка, содержащая запятую	набор	Некорректный	"Преображенская, площадь"
Строка, содержащая тире	набор	Корректный	«Зеленоград — Крюково»
Строка, содержащая точку	набор	Некорректный	«Зеленоград. Крюково»
Строка, содержащая латинские буквы	набор	Некорректный	"Mitino"
Строка, содержащая символы других языков	набор	Некорректный	"通り"
Строка, содержащая спецсимволы	набор	Некорректный	"%;$#?&*!"
