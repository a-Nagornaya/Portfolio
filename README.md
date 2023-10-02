<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>
<h1>Портфолио тестировщика</h1>
<p>В портфолио собраны учебные и тренировочные проекты, выполненные во время обучения.</p>
	
<a href='#designing-test'>Проектирование тестов</a>
<p> Тест-анализ | Ассоциативные карты | Блок-схемы |
Тест-дизайн | Классы эквивалентности | Граничные значения
Тестовая документация | Чек-листы </p>

<a href='#web-test'>Тестирование веб-приложений</a>
<p>  Пользовательский интерфейс | Тестовая документация | Чек-листы | Классы эквивалентности | Таблицы принятия решений | Баг-репорты</p>

<h2>Тестирование API</h2>
<p>  REST API | Postman</p>

<a href="#SQL-test"> Тестирование БД</a>
<p>SQL | Базы данных </p>

<a href="#avto-test"> Основы автоматизации тестирования</a>
<p>JavaScript | DevTools</p>



        
<section><h3 id="designing-test">Проектирование тестов</h3></section>
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
<details>
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
<img src='https://github.com/a-Nagornaya/Portfolio/assets/133662962/70a40e2c-d310-439e-af4d-6780351561e7' alt="Ассоциативная карта">

<br>Классы эквивалентности и граничные значения
В ходе тестирования я выделила следующий класс эквивалентности, определила граничные значения и протестировала их:

Поля ввода адреса (Откуда, Куда)

<table>
	<tr>
		<th>Название класса</th>
		<th>Тип класса</th>
		<th>Границы</th>
		<th>Тестовые данные внутри класса</th>
		<th>Тестовые данные на границах</th>
	</tr>
	<tr>
		<th>от 1 до 50 символов</th>
		<th>диапазон</th>
		<th>1, 50</th>
		<th>22 символов: "Преображенская площадь" </th>
		<th>1 символ: "П"</th>
	</tr>
	<tr>
		<th></th>
		<th></th>
		<th></th>
		<th></th>
		<th>49 символов: «Преображенская площадь Сокольническая линия красн»</th>
	</tr>
	<tr>
		<th></th><th></th><th></th><th></th>
		<th>50 символов: " Преображенская площадь, Сокольническая линия красн"</th>
	</tr>
	<tr>
		<th>от -∞ до 0</th>
		<th>диапазон</th>
		<th>0</th>
		<th>
		</th>
		<th>0 символов: пустая строка</th>
	</tr>
	<tr>
		<th>от 51 до +∞</th>
		<th>диапазон</th>
		<th>51</th>
		<th>85 символов: " Преображенская площадь, Сокольническая линия, красная ветка московского метрополитена "
		</th>
		<th>51 символ: " Преображенская площадь, Сокольническая линия красна "</th>
	</tr>
</table>
			<p>Вводимые значения</p>
			<table>
				<tr>
		<th>Название класса</th>
		<th>Тип класса</th>
		<th>Границы</th>
		<th>Тестовые данные внутри класса</th>
		</tr>
<tr>
					<th>Строка, содержащая русские буквы
					</th>
					<th>набор</th>
     <th>Корректный</th>
	<th>"Сокол" </th>
</tr>
<tr>
	<th>Строка, содержащая цифры</th>
	<th>набор</th>
	<th>Некорректный</th>
	<th>"Преображенская площадь11"</th>
</tr>
<tr>
	<th>Строка, содержащая пробел в середине текста</th>
	<th>набор</th>
	<th>Корректный</th>
	<th>"Преображенская площадь" </th>
</tr>
				<tr>
	<th>Строка, содержащая пробел в конце текста</th>
	<th>набор</th>
	<th>Корректный</th>
	<th>"Преображенская площадь " </th>
</tr>
<tr>
	<th>Строка, содержащая запятую</th>
	<th>набор</th>
	<th>Некорректный</th>
	<th>"Преображенская, площадь " </th>
</tr>
<tr>
	<th>Строка, содержащая тире</th>
	<th>набор</th>
	<th>Корректный</th>
	<th>«Зеленоград — Крюково»</th>
</tr>
<tr>
	<th>Строка, содержащая точку</th>
	<th>набор</th>
	<th>Некорректный</th>
	<th>«Зеленоград. Крюково»</th>
</tr>
<tr>
	<th>Строка, содержащая латинские буквы</th>
	<th>набор</th>
	<th>Некорректный</th>
	<th>"Mitino"</th>
</tr>
<tr>
	<th>Строка, содержащая символы других языков</th>
	<th>набор</th>
	<th>Некорректный</th>
	<th>"通り"</th>
</tr>

<tr>
	<th>Строка, содержащая спецсимволы</th>
	<th>набор</th>
	<th>Некорректный</th>
	<th>"%;$#?&*!"</th>
</tr>				
			</table>



<section><h3 id="web-test">Тестирование приложения List Boxer версии 1.98</h3></section>
<p>
	Для тестирования применяю метод черного ящика, так как к заданию была представлена только программа без исходного кода. Тестирования буду проводить вручную для этого буду применять следующие виды тестирования: функциональное тестирования, тестирование пользовательского опыта, тестирование пользовательского интерфейса.
</p>
<br>Требования к системе:<br>
<ol>
	<li>Тип операционной системы: Windows XP SP2 
	</li>
	<li>Минимальные требования к системе:</li>
 <ul>процессор - Intel Celeron 440 @ 1.00 GHz,  - ОЗУ -  1 Гб</ul>
 <ul>видеоадаптер – 64</ul>
 <ul>минимальный объем свободного места на диске 100 Кб</ul>	
</ol>
<br>Порядок тестирования: <br>
<ol>
	<li>Составление чек-листа и выделение классов эквивалентности</li>
	<li>Составление тест-кейсов</li>
	<li>Тестирование и заведение баг-репортов</li>
	<li>Подведение итогов, вывод</li>
	<li>Рекомендации</li>
</ol>
<p>1.Составление чек-листа и выделение классов эквивалентности</p>
<br>
<table>
	<tr>
		<th>№</th>
		<th>Описание проверки</th>
		<th>Результат</th>
		<th>ID баг-репорта</th>
	</tr>
	<tr>
		<th colspan="4">Общая проверка</th>
	</tr>
	<tr>
		<th>1</th>
		<th>Проверить работу кнопки Add to List</th>
		<th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>2</th>
		<th>Проверить работу кнопки Clear List</th>
		<th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>3</th>
		<th>Проверить меню выбора фильтра</th><th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>4</th>
		<th>Проверить выбор сортировки</th><th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>5</th>
		<th>Проверить выбор режима</th><th>PASSED</th><th></th>
	</tr>
	<tr><th>6</th> <th>Проверить кнопку меню File Open (Список текстового формата, Файл-картинка/видео/Gif, Пустой список, Большой файл, Список с недопустимыми значения данных)</th>
		<th>FAILED</th>
		<th>BUG-301</th>
	</tr>
	<tr>
		<th>7</th>
		<th>Проверить кнопку меню File Save As (Список текстового формата, Пустой список, Большой файл, Список с недопустимыми значения данных)</th><th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>8</th> <th>Проверить кнопку меню File Exit (Список текстового формата, Пустой список, Список с недопустимыми значения данных, Список с недопустимыми значения данных)</th><th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>9</th> <th>Проверить кнопку меню Edit Undo (Поменять range, Поменять сортировку, Добавить значения, удалить и заменить значения, поменять режим)</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>10</th>
		 <th>Проверить действие клавиш ctrl+z (Поменять range, Поменять сортировку, Добавить значения, удалить и ищменить значения, поменять режим)</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>11</th> <th>Проверить кнопку меню Help Contents</th> <th>FAILED</th> <th>BUG-302</th>
	</tr>
	<tr>
		<th>12</th>
		<th>Проверить кнопку меню Help About ListBoxer</th>
		<th>FAILED</th> <th>BUG-303</th>
	</tr>
	<tr>
		<th>13</th> <th>Проверить кнопку ? для вызова контекстной справки</th>
		<th>FAILED</th> <th>BUG-302</th>
	</tr>
	<tr>
		<th>14</th> <th>Проверить кнопку x.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>15</th> <th>Проверить на наличие грамматических ошибок в меню программы.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th colspan="4">Функциональность при алфавитном режиме</th>
	</tr>
	<tr>
		<th>16</th> <th>Ввести буквы латиницей.</th>  <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>17</th> <th>Ввести буквы кириллицей.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>18</th> <th>Ввести буквы латиницей и кириллицей.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>19</th> <th>Ввести буквы в разных регистрах.</th><th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>20</th> <th>Ввести цифры.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>21</th> <th>Ввести буквы и цифры.</th>  <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>22</th> <th>Ввести отрицательные числа.</th> <th>PASSED</th><th></th>
	</tr>
	<tr> <th>23</th> <th>Ввести буквы от 1 до 8.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>24</th> <th>Ввести намного больше 8 букв.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>25</th> <th>Пустое поле.</th> <th>FAILED</th> <th>BUG-304</th>
	</tr>
	<tr>
		<th>26</th> <th>Ввести 9 букв.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>27</th> <th>Ввести 7 букв.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>28</th> <th>Ввести символы.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>29</th> <th>Ввести рисунок.</th> <th>PASSED</th><th></th>
	</tr>
	<tr> <th>30</th> <th>Ввести эмодзи.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>31</th> <th>Ввести двоичное число.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>32</th> <th>Ввести пробел.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th colspan="4">Функциональность при числовом режиме</th>
	</tr>
	<tr>
		<th>33</th> <th>Ввести буквы </th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>34</th> <th>Ввести число от 0 до 9999</th>  <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>35</th> <th>Ввести число намного больше 9999</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>36</th> <th>Ввести отрицательное число</th><th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>37</th> <th>Ввести буквы и числа</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>38</th> <th>Пустое поле</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>39</th> <th>Ввести пробел</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>40</th> <th>Ввести символы</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>41</th> <th>Ввести рисунок.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>42</th> <th>Ввести эмодзи.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>43</th> <th>Ввести двоичное число.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>44</th> <th>Ввести 9998</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>45</th> <th>Ввести 10000</th> <th>FAILED</th> <th>BUG-305</th>
	</tr>
	<tr>
		<th colspan="4">Функциональность при смешанном режиме</th>
	</tr>
	<tr>
		<th>46</th><th>Ввести числа от 1 до 8</th><th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>47</th> <th>Ввести число от 0 до 9999</th>  <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>48</th> <th>Ввести число намного больше 9999</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>49</th> <th>Ввести 10000</th> <th>FAILED</th> <th>BUG-305</th>
	</tr>
	<tr>
		<th>50</th> <th>Ввести 9998</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
 <tr>
	 <th>51</th> <th>Ввести 7 букв</th><th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>52</th> <th>Ввести 9 букв</th><th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>53</th> <th>Ввести намного больше 9 букв.</th><th>PASSED</th><th></th>
 </tr>
		<th>54</th> <th>Ввести отрицательное число</th><th>PASSED</th><th></th>
	</tr>
 <tr>
		<th>55</th> <th>Ввести двоичное число.</th> <th>PASSED</th><th></th>
	</tr>
 <tr>
		<th>56</th> <th>Пустое поле</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>57</th> <th>Ввести пробел</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>58</th> <th>Ввести буквы и числа</th> <th>PASSED</th><th></th>
	</tr>
 <tr>
	 <th>59</th> <th>Ввести буквы на разных языках</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>60</th><th>Ввести буквы в разных регистрах</th><th>PASSED</th><th></th>
 </tr>
	<tr>
		<th>61</th> <th>Ввести символы</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>62</th> <th>Ввести рисунок.</th> <th>PASSED</th><th></th>
	</tr>
	<tr>
		<th>63</th> <th>Ввести эмодзи.</th> <th>PASSED</th><th></th>
	</tr>
 <tr>
	 <th colspan="4">Проверка фильтров: в алфавитном режиме</th>
 </tr>
 <tr>
	 <th>64</th> <th>Фильтр “none” (ввести буквы, ввести цифры, ввести символы)</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>65</th> <th>Фильтр “All” (ввести буквы, ввести цифры, ввести символы)</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>66</th> <th>Фильтр “a-m” (ввести любые буквы от a до k, ввести букву m, ввести букву n, ввести любые буквы от n до z)</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>67</th> <th>Фильтр “ n-z” (ввести любые буквы от a до k, ввести букву m, ввести букву n, ввести любые буквы от o до z)</th> <th>PASSED</th><th></th>
 </tr>
  <tr>
	 <th colspan="4">Проверка фильтров: в числовом режиме</th>
 </tr>
<tr>
	 <th>68</th> <th>Фильтр “none” (ввести буквы, ввести цифры, ввести символы)</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>69</th> <th>Фильтр “0-100” (ввести 0, ввести 100, ввести любое число от 1 до 99, ввести 101, ввести любое число от 102 до 9999)</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>70</th> <th>Фильтр “101-200” (ввести 101, ввести 200, ввести любое число от 102 до 199, ввести число 201, ввести любое число от 201 до 9999, ввести число 100, ввести любое число от 0 до 99)</th>  <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>71</th> <th>Фильтр “201-300” (ввести 201, ввести 300,
ввести любое число от 202 до 299,
ввести 200, ввести любое число от 0 до 199, ввести 301, ввести любое число от 302 до 9999)
</th><th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>72</th> <th>Фильтр “301-9999” (ввести 301, ввести 300, ввести любое число от 0 до 299,
ввести любое число от 302 до 9999, ввести 10000)
</th><th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th colspan="4">Проверка фильтров: в смешанном режиме</th>
 </tr>
 <tr>
	 <th>73</th> <th>провести проверку фильтров таким же образом, как в алфавитном и цифровом режиме</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>74</th> <th>ввести в поле в начале буквы, а потом цифры для каждого фильтра</th> <th>PASSED</th><th></th>
 </tr>
 <tr>
	 <th>75</th> <th>ввести в поле в начале цифры, а потом буквы для каждого фильтра</th>
	 <th>FAILED</th> <th>BUG-307</th>
 </tr>	
</table>

<p>2.Составление тест-кейсов</p>
<br>
<p>ID-1: Общая проверка работы интерфейса программы и поиск грамматических ошибок</p>
<p>ОР: Все кнопки работают корректно.</p>
<p>Шаги:</p>
<ol>
	<li>Открыть программу</li>
	<li>Проверить работу кнопок в соответствии с чек-листом</li>
</ol>
<p>Результат: FAILED</p>
<p>ID баг-репорта: BUG-301, BUG-302, BUG-303</p>

<p>ID-2: Проверка функциональности в алфавитном режиме</p>
<p>ОР: Отражается часть списка, состоящая из буквенных символов верхнего и нижнего регистра латинского алфавита, но не более 8, ввод других символов не допускается</p>
<p>Шаги:</p>
<ol>
	<li>Открыть программу</li>
	<li>Проверить работу кнопок в соответствии с чек-листом</li>
</ol>
<p>Результат: FAILED</p>
<p>ID баг-репорта: BUG-304</p>

<p>ID-3: Проверка функциональности в числовом режиме</p>
<p>ОР: Отражается часть списка, состоящая из цифр в диапазоне от 0 до 9999, ввод других символов не допускается</p>
<p>Шаги:</p>
<ol>
	<li>Открыть программу</li>
	<li>Проверить работу кнопок в соответствии с чек-листом</li>
</ol>
<p>Результат: FAILED</p>
<p>ID баг-репорта: BUG-305</p>


<p>ID-4: Проверка функциональности в смешанном режиме</p>
<p>ОР: Отражается весь список, состоящая из буквенных символов верхнего и нижнего регистра латинского алфавита, но не более 8, а также цифр в диапазоне от 0 до 9999, ввод других символов не допускается</p>
<p>Шаги:</p>
<ol>
	<li>Открыть программу</li>
	<li>Проверить работу кнопок в соответствии с чек-листом</li>
</ol>
<p>Результат: PASSED</p>


<p>ID-5: Проверка функциональности фильтров в алфавитном режиме</p>
<p>ОР: Отражается часть списка, состоящая из буквенных символов верхнего и нижнего регистра латинского алфавита</p>
<p>Шаги:</p>
<ol>
	<li>Открыть программу</li>
	<li>Проверить работу кнопок в соответствии с чек-листом</li>
</ol>
<p>Результат: PASSED</p>


<p>ID-6: Проверка функциональности фильтров в числовом режиме</p>
<p>ОР: Отражается часть списка, состоящая из цифр в диапазоне от 0 до 9999</p>
<p>Шаги:</p>
<ol>
	<li>Открыть программу</li>
	<li>Проверить работу кнопок в соответствии с чек-листом</li>
</ol>
<p>Результат: FAILED</p>
<p>ID баг-репорта: BUG-305</p>


<p>ID-7  Проверка функциональности фильтров в смешанном режиме</p>
<p>ОР: Отражается часть списка, согласно выбранному фильтру</p>
<p>Шаги:</p>
<ol>
	<li>Открыть программу</li>
	<li>Проверить работу кнопок в соответствии с чек-листом</li>
</ol>
<p>Результат: FAILED</p>
<p>ID баг-репорта: BUG-307</p>

<p>3.Тестирование и заведение баг-репортов</p>
<br>
<details>
<summary>BUG-301: Не работает копка меню File Open</summary>
Ожидаемый результат: Открываются сохраненные списки.
<br>
Фактический результат: Не работает копка меню File Open, не открывается ни один вид сохраненных списков. 
<br>
Окружение:
<p>
Windows 11 22H2
<br>
Разрешение экрана: 1920x1080
<br>
</p>
<br>
Приоритет-высокий.

</details>

<br>
<details>
<summary>BUG-302: Не корректно работают кнопки Help Contents и ?.</summary>
Ожидаемый результат: Открывается информация в браузере.
<br>
Фактический результат: Не открывается информация в браузере.
<br>
Окружение:
<p>
Windows 11 22H2
<br>
Разрешение экрана: 1920x1080
<br>
</p>
<br>
Приоритет-низкий.

</details>

<br>
<details>
<summary>BUG-303: Информация о версии программы в кнопке Help About ListBoxer не верная. </summary>
Ожидаемый результат: При нажатии Help About ListBoxer указана верстия 1.98.
<br>
Фактический результат: Фактическая информация верстия- 1.89.
<br>
Окружение:
<p>
Windows 11 22H2
<br>
Разрешение экрана: 1920x1080
<br>
</p>
<br>
Приоритет-низкий.

</details>

<br>
<details>
<summary>BUG-304: При вводе пустого поля в алфавитном режиме в список добавляется пустая строка.</summary>
Ожидаемый результат: При вводе пустого поля в список ничего не добавляется.
<br>
Фактический результат: При вводе пустого поля в алфавитном режиме в список добавляется пустая строка.
<br>
Окружение:
<p>
Windows 11 22H2
<br>
Разрешение экрана: 1920x1080
<br>
</p>
<br>
Приоритет-низкий.

</details>

<br>
<details>
<summary>BUG-305: При вводе 10 000 в цифровом и смешанном режиме происходит ошибочное добавление в список.</summary>
Ожидаемый результат: При вводе 10 000 программа выдает ошибку.
<br>
Фактический результат: При вводе 10 000 в цифровом и смешанном режиме происходит ошибочное добавление в список.
<br>
Окружение:
<p>
Windows 11 22H2
<br>
Разрешение экрана: 1920x1080
<br>
</p>
<br>
Приоритет-низкий.

</details>

<br>
<details>
<summary>BUG-306: Работа фильтра в числовом режиме допускает 10000.</summary>
Ожидаемый результат: При вводе 10 000 программа выдает ошибку.
<br>
Фактический результат: : Работа фильтра в числовом режиме допускает 10000, при диапазоне значений от 0 до 10 000. 
<br>
Окружение:
<p>
Windows 11 22H2
<br>
Разрешение экрана: 1920x1080
<br>
</p>
<br>
Приоритет-низкий.

</details>

<br>
<details>
<summary>BUG-307: Работа фильтра в смешанном режиме не корректна.</summary>
Ожидаемый результат: При фильтрации в смешанном режиме, при вводе сначала цифр, а потом букв данный пункт попадает в оду из классификаций. 
<br>
Фактический результат: При вводе сначала цифр, а потом букв данный пункт не попадает ни в оду из классификаций.
<br>
Окружение:
<p>
Windows 11 22H2
<br>
Разрешение экрана: 1920x1080
<br>
</p>
<br>
Приоритет-высокий.

</details>
<br>
<p>4.Подведение итогов, вывод</p>
<p>
	Данное тестирование я проводила вручную, но в дальнейшем его можно автоматизировать. При автоматизации можно использовать метод «запись- воспроизведение».
Анализируя результаты тестирования я пришла к выводу, что данная программа нуждается в доработке, по причине наличия большого количества багов. Многие из них не влияют на функциональность приложения, но некоторые ведут к потере информации.

</p>
<p>5.	Рекомендации</p>
<P>
	Нужно обратить внимание на баги с высоким приоритетом (BUG-301, BUG-307), так как эти ошибки ведёт к потере информации введенной пользователем или ее некорректному отображению.
</P>
<br><br><br>



<section><h3 id="SQL-test">Тестирование БД</h3></section>
<p>
В ходе обучения я освоила язык SQL, отрабатывала я данный нывык на тренажере hackerrank  и дополнительно прошла курс Яндекс.Практикум "SQL-Basic". В ходе обученя я получила сертификат: 
<details>
<summary>SQL (Basic) Certificate</summary>
	<img src='https://github.com/a-Nagornaya/Portfolio/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202023-09-29%20205315.png'>
</details>
<p>Вот несколько примеров выполненных задач:</p>
<p>Задача 1</p>
<p>Саманта вводила данные в таблицу заработной платы в таблицу EMPLOYEES, но у нее не работла кнопка 0 и она не заметила этого, нужно посчитать разницу между актульной и ошибочной ЗП (SALARY-графа с ЗП). Ниже привожу скрин с выполненной задачей и подробным условием.  </p>
<p>Решение</p>
<pre><code>
	SELECT CEIL(AVG(SALARY)-AVG(REPLACE(SALARY, '0', '')))
	FROM EMPLOYEES;
	/* выбераю наименьшее целое число (сeil), полученное в результате вычитания из 
	среднего арифметического (avg) фактической ЗП и среднего арифметического введенной ЗП,
	но где 0 замененн на ' '(replace)*/
</code></pre>
<details>
<summary>Скрин задачи</summary>
	<img src='https://github.com/a-Nagornaya/Portfolio/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202023-09-28%20094013.png'>
</details>
<br>

<p>Задача 2</p>
<p>Напишите запрос, который выводит список имен сотрудников (name) для таблицы сотрудников (EMPLOYEE), которые получаю ЗП (SALARY) больее 2000 и работают менее 10 месяцев (MONTHS). Отсортируйте по возрастанию ID (EMPLOYEE_ID). Ниже привожу скрин с выполненной задачей и подробным условием.
</p>
<p>Решение</p>
<pre><code>
	SELECT NAME FROM EMPLOYEE WHERE
	SALARY > 2000 AND MONTHS < 10
		ORDER BY EMPLOYEE_ID;
		/* выбераю имена сотрудников, которые соответствуют условиям и сортирую по ID,
		условия сортировки дополнительно не прописываю, так как по умолчанию сортировка будет нужная
		*/
</code></pre>
		<details>
<summary>Скрин задачи</summary>
	<img src='https://github.com/a-Nagornaya/Portfolio/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202023-09-27%20223520.jpg'>
</details>
<br>
<p>Задача 3</p>
<p>Создайте следующие два результирующих набора:
Запросите в алфавитном порядке список всех имен в OCCUPATIONS, сразу за которым следует первая буква каждой профессии в скобках (т. е. заключена в скобки).
Запросите количество повторений каждой профессии в OCCUPATIONS. Отсортируйте вхождения в порядке возрастания</p>
<p>Решение</p>
<pre><code>
select concat(name, '(', SUBSTR(occupation, 1, 1),')') 
from occupations 
order by name;
select 'There are a total of ' ,count(occupation) ,concat(lower(occupation), 's.') 
from occupations
group by occupation 
order by count(occupation) , occupation ;
</code></pre>
<details>
<summary>Скрин задачи</summary>
	<img src='https://github.com/a-Nagornaya/Portfolio/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202023-09-30%20193700.png'>
</details>
<br>
<p>Задача 4</p>
<p>Отобразите дату, первый день месяца, название пиццы и количество пицц в заказе. Отберите заказы только за февраль и с количеством пицц в заказе, не равным одному.</p>
<p>Решение</p>
<pre><code>
SELECT date, name, quantity, DATE_TRUNC('month', date) 
FROM pizza 
WHERE  DATE_TRUNC('month', date) = '2022-02-01' AND quantity != 1;
</code></pre>
<details>
<summary>Скрин задачи</summary>
	<img src='https://github.com/a-Nagornaya/Portfolio/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202023-10-02%20094328.png'>
</details>
<br>






<section><h3 id="avto-test">Основы автоматизации тестирования</h3></section>
<strong>Автоматизируй тест-кейс для Яндекс.Маршрутов.</strong>
<p>Найди нужные селекторы на стенде: https://qa-routes.praktikum-services.ru/
<br>
Шаги:<br>
<ol>
<li> Ввести «Время начала поездки» — 16:10.</li>
<li>В поле «Откуда»: Усачева, 3.</li>
<li>В поле «Куда»: Комсомольский проспект, 18.</li>
<li>Выбрать режим «Свой».</li>
<li>Выбрать вид транспорта: самокат.</li>
</ol>
ОР: Текст появившегося результата начинается со слова «Самокат».
</p>
<br>
Решение:<br>
Селекторы:
<table>
	<tr>
		<th>Элемент</th> <th>Селектор</th>
	</tr>
	<tr>
		<th>Поле «Часы»</th> <th>#form-input-hour</th>
	</tr>
	<tr>
		<th>Поле «Минуты»</th> <th>#form-input-minute</th>
	</tr>
	<tr>
		<th>Поле «Откуда»</th> <th>#form-input-from</th>
	</tr>
	<tr>
		<th>Поле «Куда»</th> <th>#form-input-to</th>
	</tr>
	<tr>
		<th>Режим «Свой»</th> <th>#form-mode-custom</th>
	</tr>
	<tr>
		<th>Транспорт «Самокат»</th> <th>#form-type- scooter</th>
	</tr>
	<tr>
		<th>Строка результата</th> <th>#result-time-price</th>
	</tr>
</table>


<br> Автотест:<br>
<pre><code>const puppeteer = require('puppeteer'); 

const URL_TEST = 'https://qa-routes.praktikum-services.ru/';

async function testScooterResult() {
    console.log('Запуск браузера');
    const browser = await puppeteer.launch({headless: false, slowMo: 100});

    console.log('Новая вкладка браузера');
    const page = await browser.newPage();

    console.log('Переход по ссылке');
    await page.goto(URL_TEST);

    console.log('Шаг 1: ввод часов и минут');
    const hoursInput = await page.$('# form-input-hour');
    await hoursInput.type('16');

    const minutesInput = await page.$('# form-input-minute');
    await minutesInput.type('10');

    console.log('Шаг 2: заполнение поля Откуда');
    const fromInput = await page.$('# form-input-from');
    await fromInput.type('Усачева, 3');

    console.log('Шаг 3: заполнение поля Куда');
    const toInput = await page.$('# form-input-to');
    await toInput.type('Комсомольский проспект, 18');

    console.log('Шаг 4: выбор режима Свой');
    const routeMode = await page.$('#form-mode-custom');
    await routeMode.click();

    console.log('Шаг 5: выбор вида транспорта');
    const typeOfTransport = await page.$('#form-type-scooter');
    await typeOfTransport.click();

    console.log('Ожидание элемента с результатом');
    await page.waitForSelector('#result-time-price')

    console.log('Получение строки с результатом');
    const text = await page.$eval('#result-time-price'', element => element.textContent);

    console.log('Проверка условия тест-кейса');
        if (text.startsWith('Самокат')) {
        console.log('PASSED');
    } else {
          console.log(`FAILED`)
    }

    console.log('Закрытие браузера');
    await browser.close();
}
</code></pre>
<strong>Автоматизируй тест-кейс для Demo Web Shop (tricentis.com), применив нужные селекторы.</strong>
<p>Найди нужные селекторы на сайте: [https://qa-routes.praktikum-services.ru/](https://demowebshop.tricentis.com/), просмотреть можно с помошью DevTools
<br>
	Предусловие:<br>
Перейти на страницу DemoWebShop.<br>

Шаги:<br>
<ol>
<li> Ввести «Computer» в поисковую строку.</li>
<li>Нажать кнопку «Найти».</li>
</ol> <p>ОР: Выполнен переход на страницу выдачи поиска и результат поиска непустой.
</p>
<br>
Решение:<br>
Селекторы:
<table>
	<tr>
		<th>Элемент</th> <th>Селектор</th>
	</tr>
	<tr>
		<th>Поисковая строка</th> <th>#small-searchterms</th>
	</tr>
	<tr>
		<th>Кнопка «Search»</th> <th>.button[type=submit]</th>
	</tr>
	<tr>
		<th>Результат поиска</th> <th>.search-results</th>
	</tr>
	
</table>
<br> Автотест:<br>
<pre><code>
	const puppeteer = require('puppeteer');

async function testDemoShop () {
    console.log('Запуск браузера');
    const browser = await puppeteer.launch();

    console.log('Создание новой вкладки в браузере');
    const page = await browser.newPage();

    console.log('Переход на страницу tricentis.com');
    await page.goto('tricentis.com');

    console.log('Ввод текста "Computer" в поисковую строку');
    const searchField = await page.$('#small-searchterms ');
    await searchField.type('Computer');

    console.log('Клик в кнопку "Найти"');
    const searchButton = await page.$('.button[type=submit]');
    await searchButton.click();
    
    console.log('Ожидание перехода в страницу поисковых результатов');
    await page.waitForNavigation();
    
    console.log('Получение элементов результата поиска');
    const result = await page.$('.search-results');
    
    console.log('Сравнение');
    if (result == null) {
        console.log('Результаты поиска не найдены');
    } else {
        console.log('Результаты поиска отобразились');
    }
    
    console.log('Закрытие браузера');
    await browser.close();
};

</code></pre>
</body>
</html>

