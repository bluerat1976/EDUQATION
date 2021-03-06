## Функциональное программирование в контексте класса. Первый шаг к ООП. 


> Если рассматривать методы как "устройства" выполняющие определенные операции, способные принимать и возвращать результат, то значения - могут рассматриваться как некоторые "вещества" выходящие из и входящие в те устройства.


* Дд

* Предположим что наш класс "WaterProducerConsumerApp" содержит ряд приборов (методов) которые предназначены для воды. 
* В


```

| TAP | ---> "volume temperature" ---> | HEATER | ---> "volume temperature" ---> | 

```

* Рассмотрим пример простого класса с методом "main()"
  
    ```java
    public class WaterProducerConsumerApp {
        
        
        public static void main(String[] args) {

        }

        public 
    }
    ```
    метод **main()** специальный метод который мы только объявляем, а программа "сама" его вызывает каким-то магическим пока для нас трюком.
    Всматриваясь в формулу данного метода, если вам не особо знакомы концепции ООП, необходимо пока обратить внимание на:
     1. имя метода **main()**, используйте camelCase (напр - myMethod(), getData(), toMoreComplexData()) 
     2. аргумент **args** - тип String[]
     3. ничего не возвращает - тип возврата **void**
     4. доступно прямо из этого класса **static**
     5. тело того что будет метод делать **{ ... }**   
    Для начинающего - установим пока это простое правило: В НЕ КЛАССА метод НЕ объявлять! 

    В коде  что выше, территория класса **CalculatorMethodsApp** задана маркерами "CLASS BEGIN", "CLASS END"

    Для начинающего - класс это коробка в которую мы "устанавливаем" метод благодаря ключевому слову "static'

* Класс **CalculatorMethodsApp** назван так, потому что он будет содержать логику вычислений / операций, который выполняет простой карманный калькулятор
 
* Добавим метод - "provider" (поставщик) воды
 
  ```java
  static void printResult(int result) {
      System.out.printf("result: %08d\n",result);
  }
  ``` 
  данный метод ничего не возвращает, принимает целое число в переменную (аргумент) **result** и выводит значение в формате - на экран
  
   -  Хотите проверить метод? 
  ```java
    public static void main(String[] args) {
        printResult(0);
        printResult(10);
        printResult(99999999);
        printResult(999999999);
        printResult(-100);
    }
  ```
  обратите внимание на вызов - мы просто обращаемся к методу по имени, так как он в той же коробке что и вызывающий его метод **main()**

* Как вы видите наш метод **printResult(int result)** не может работать в формате с числами больше 8 цифр - так как форматирование не срабатывает. Поэтому требуется внутри метода добавить условие которое будет выводить "ERROR" если кол-во требуемых знаков для вывода целого значения **result** превышает 8

* Добавим метод который "украсит" наш вывод на экран, при этом он не требует аргументов (так как всегда выполняет одно и то же - без внешнего вмешательства), и который ничего не вернет - void
    ```java
    static void printDivider() {
        System.out.println("################");
    }
    ```   
    проверим в **main()**

    ```java
    printDivider();
    printResult(10);
    printDivider();
    ```

    и видим 

    ```
    ################
    result: 00000010
    ################
    ```

* добавляем метод сложения двух чисел, принимает два целых, возвращает один целый результат
    ```java
    static int add(int a, int b) {
        int r = a + b;
        return r;
    }
    ```  
    Как понимать **return**? в момент когда метод выполняет эту строку, его выполнение завершается и значение возвращается в то место откуда метод вызвали, например в
    
    ```java
    printDivider();
    printResult( add(1,2) );
    printDivider();
    ```
    **add(1,2)** вернет результат в **printResult( ... )** вместо **...**

* Требуется:
  1. Добавить еще методы **int sub(int a, int b)**, **int mul(int a, int b)**, **int div(int a, int b)** - которые выполняют соответственно - вычитание, умножение, деление
  2. Добавить еще метод **int pow(int v, int e)** - возведения в степень т.е. - например ```pow(10,3)``` это ```1000```
  3. После этого в **main()** используя все эти методы - решить и вывести следующую формулу ```1 + 2^3 * 3 / 4 - 5``` (где 2^3 - два в 3-й степени)

