## Функциональное программирование в контексте класса. Статические методы

* Представьте, что где-то в памяти есть карта, которая
  представляет собой размещение множества объектов на заданной поверхности (земле).
  "Поле" карты имеет размеры "hsize" x "vsize", в целых единицах - метрах. 
   По двум переменным (x, y) задано положение наблюдателя на карте (один человек).
   По двум переменным (cx, cy) задано положение здания (сооружения) которое он видит.
* Требуется:
 1. Создать класс приложения с **main()** и правильно его назвать, исходя из того что от вас потребуют сделать ниже.
 2. Объявить метод **printMap()** который на основе вышеупомянутых переменных выводит карту примерно так:
    ```
                         N
                         ^
                1  2  3  4  5  6  ...
            1   .  .  .  .  .  .  .     
            2   .  .  .  .  .  .  .     
            3   .  .  .  .  .  .  .     
    W <     4   .  .  O  .  C  .  .     > E
            5   .  .  .  .  .  .  .     
            6   .  .  .  .  .  .  .     
            7   .  .  .  .  .  .  .     
            .. 
                         v
                         S 
    ```

    Где N,E,S,W - географические направления. Они должны равняться строго по центру длины как горизонтального так и вертикального направления. Периметр должен быть отмечен шагами 1,2,... до hsize ( vsize )     

    На карте нанесены "O" - наблюдатель и "C" - объект

 3. Рассчитать и отобразить площадь карты (1 единица = 1 метр) / в кв. метрах, при помощи метода **printMapArea()**
 4. Используя географические направления (N, NE, E, SE, S и т. Д.) Вывести направление в котором
    должен смотреть наблюдатель чтобы увидеть сооружение, при помощи метода **printViewDirection()**

 5. БОНУС, рассчитать и отобразить расстояние по тригонометрической формуле
    между наблюдателем и сооружением при помощи метода **printDistanceToObject()**

* !!! ВНИМАНИЕ, в условиях не указаны ни аргументы ни тип возврата, вам решать какую сигнатуру использовать при объявление методов!
* !!! НАЧАТЬ ПРОВЕРКУ с значений: 
 
        ```
        hsize = 10, vsize = 10, x = 3, y = 4, cx = 5, cy = 4.
        ```

        Для этих условий поверхность будет = 100 квадратных метров, чертеж будет отображаться
        аналогично приведенному ниже, конструкция будет для наблюдателя
        видна в направлении E (восток) и расстояние между наблюдателем и сооружением составит 2 единицы (метры)
        как показано на карте.

        ```
                            x    cx
                        1  2  3  4  5  6  ...hsize -->
                    1   .  .  .  .  .  .  .     .
                    2   .  .  .  .  .  .  .     .
                    3   .  .  .  .  .  .  .     .
            cy,y    4   .  .  O  .  C  .  .     .
                    5   .  .  .  .  .  .  .     .
                    6   .  .  .  .  .  .  .     .
                    7   .  .  .  .  .  .  .     .
                    ..  
                vsize   .  .  .  .  .  .  .     .
                    |
                    |
                    v
        ```