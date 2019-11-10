##

> Знали ли вы что **margin** с отрицательными значениями действует иначе - притягивая соседние элементы
> Блочный элемент по умолчанию получает значение **width** (ширины) "auto", что означет что брауэер вычисляет его ширину в зависимости от контекста в котором он находится (родительский размер, отступы, поток, режим отображения)


--- 

* Посмоторите на то как должен выглядеть готовый [результат](./result.png). В этом примере мы нарисовали дом обведенный точечным контуром, крышу, стены и основание. Все элементы блочные. На основе исходника [index](./index.html) выполнить следующие пункты :
    1. Отцентровать в горизонтальном направлении все блоки
    2. Нарисовать крышу дома элементом "roof' (создайте триугольник за счет свойств "border")
    3. Нарисовать стены и основание, обратите внимение что основание ШИРЕ дома на 40px, нарисуйте основание дома (foundation) учитывая то что для этого элемента вы не имеете право фиксировать ширину (width). Ее значение должно остаться в режиме "auto"
    4. Ответить на вопрос: - почему над крышей есть отступ?
    5. Ответить на вопрос: - Чему равняется высота всего дома? 

БОНУС!!!    на данный момент в HTML 2 див с классом "floor" отключены, отключите див "walls", и вместо него вкл. "floor" так чтобы дом был 2-х этажный и это четко было видно в результате