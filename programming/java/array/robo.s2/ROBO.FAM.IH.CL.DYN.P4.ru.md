## Классы. Динамическое использование - объекты. 
## Структуры данных. Массивы

### Фабрика роботов [часть 4]


* Самая большая проблема нашего приложения до этого момента - это что роботы не знают друг о друге и не в курсе того что происходит на карте. Потому необходимо добавить объект роль которого будет "сконцентрировать" всю информацию об объектах находящихся на карте.

* Предположим у нас есть новый тип - объект класса **RobotControlBase**, этот класс СОЗДАЕТ один всего лишь объект соответствующий "базы роботов" (т е - пункт управления). Это неподвижный объект с координатами в 2D пространстве. База содержит массив **entities** вещей имеющие 2D координаты (т е - роботов, станций, ...)

  ```java
  public class RobotControlBase /* ??? */ {
      private Has2DCoordinatesInterface[] entities;

      public Has2DCoordinatesInterface set(int index, Has2DCoordinatesInterface entity) { /* ... */ }
      public int add(Has2DCoordinatesInterface entity) { /* ... */ }
      public Has2DCoordinatesInterface get(int index) { /* ... */ }

      public String toString() { /* ... */ }
  }
  ```

  К сожалению база не имеет продвинутое железо, по этому она может "запомнить" лишь 5 вещей, добавьте конструктор таким образом чтобы он инициализировал массив из новых 5 ячеек (по дефолту в них - **null**).
  ОБРАТИТЕ ВНИМАНИЕ НА СПЕЦИАЛИЗИРОВАННЫЕ get/set! 

  - метод **set(int index, Has2DCoordinatesInterface entity)** принимает индекс ячейки массива в которую необходимо "запомнить" переданную вещь (**entity**) возвращает то значение что было ДО этого в массиве **entities** на том месте!
  - метод **add(Has2DCoordinatesInterface entity)** добавляет в "продолжении" переданную вещь. Что имеется в виду, представим себе что массив **entities** пустой
    ```
     0       1       2       3       4
    [null  ][null  ][null  ][null  ][null  ]
    ``` 
    после выполнения **add(robot1)**
    ```
     0       1       2       3       4
    [robot1][null  ][null  ][null  ][null  ]
    ``` 
    после выполнения **add(robot2)**
    ```
     0       1       2       3       4
    [robot1][robot2][null  ][null  ][null  ]
    ``` 

* У зарядной станции есть новый метод **boolean charge(HasBatteryInterface chargeable)** который будет при помощи цикла **while** ( цикл внутри метода ), поднимать заряд любого объекта с батареей (в том числе робота) до 100%.
 
 ВНИМАНИЕ! при заряде роботов от **BetaRobot** и выше один процент батареи станции - способен преобразоваться в 10% заряда батареи робота!

 ВНИМАНИЕ! станция может заряжать только если у нее в резерве как минимум 5% заряда, иначе метод **charge(...)** ничего не делает и возвращает **false**
 
 ВНИМАНИЕ! станция может заряжать только то устройство ( робота ) координаты которого совпадают с координатами станции (т е - робот должен быть в том месте где зарядная станция) 

---

* Создать тест который:
  1. Установит станцию в x/y - 10/10 с зарядом в 100% и попытается зарядить бета робота который в x/y - 20/20 (50% заряда) - не должно работать
  2. Передвинет того же робота в 10/10 и начнет зарядку - процесс зарядки должен запустится а так же по окончанию станция должна иметь 94% а робот 100% заряда!
  3. Попытается зарядить того же робота еще раз - так как он уже заряжен - процесс зарядки не должен идти!
      