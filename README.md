# Multi-Currency wallet

## Запуск

### Консольное приложение

Перейдите в папку liptSoft/Ignatov/wallet и запустите main WalletTest.java:

```bash
javac -d bin -cp ../../../../lib/junit-4.13.1.jar;.  WalletTest.java
```

```bash
java -classpath ./bin WalletTest
```

…или просто откройте Intellij IDEA, добавьте “lib” (junit) в classpath → Edit configuration и настройте приложение следующим образом

![Untitled](ReadME/1.png)

Тогда вы получите поведение, как в условии задания. Приложение завершается либо вводом некорректной команды, либо выставлением флага прерывания (ctrl + D).

### Тесты

Так же есть возможность запустить тесты (они находятся в WalletTest.java), проверяющие поведение функций для консольного приложения. Для этого можно опять зайти в Intellij IDEA и настроить Junit test следующий образом (в Edit configuration).

![Untitled](ReadME/2.png)

Или в консоли:

```bash
javac -cp ../../../../lib/junit-4.13.1.jar;. WalletTest.java

java -cp ../../../../lib/junit-4.13.1.jar;../../../../lib/hamcrest-core-1.3.jar;. org.junit.runner.JUnitCore WalletTest

```

### Банк

Кроме того, в проекте c помощью RMI реализован банк, в котором каждый пользователь, подключившись к серверу, может завести кошелек и сделать любую операцию определенную в интерфейсе Wallet. Для того, чтобы увидеть пример, как это работает, запустите main Server.java, а после этого main Client.java. 

### Тесты для банка

Проверить правильность работы банка можно, запустив тесты (BankTest.java).

## О проекте

## Features:

- Реализован многовалютный кошелёк, в котором можно проводить следующие операции:  
    
  * add currency <currency> — добавить валюту currency в кошелек  
    
  * deposit <amount> [currency] — внести amount денег в валюте currency или в первой добавленной, если не указана
    
  * withdraw <amount> [currency] — снять amount денег в валюте currency или в первой добавленной, если не указана
    
  * set rate <currency 1> <currency 2> — установить курс между двумя валютами кошелька
    
  * convert <amount> <currency 1> to <currency 2> — конвертировать amount денег в валюте currency 1 в деньги currency 2 согласно курсу
    
  * show balance — показать текущий баланс для каждой валюты кошелька
    
  * show total [in currency] — показать текущий баланс переведенный в валюту currency или в первую добавленную, если не указана

    
- Реализованы тесты для операций с валютами
- Валюты, добавленные в кошелек, помнят, в каком порядке они добавляются, поэтому при желании интерфейс wallet можно легко дополнить функциями, показывающими историю операций
- Консольное приложение не кидается в пользователя исключениями, а лишь печатает ошибку на экран, если что-то пошло не так
- Банк для создания кошельков несколькими клиентами (приложениями) и операций с ними
- Реализованы тесты для банка (в том числе тесты на многопоточность) и кошелька (покрыты все публичные методы кроме getBalanceIn and start)
- Поддерживается чтение команд с любого Readable в том числе есть возможность прочитать команды из файла (в проекте приложены примеры тестов, которые должны проходить (shouldPass) и завершаться с сообщением об ошибке (shouldFail))

## Пример работы консольного приложения

Ввод

```
add currency ruble
deposit 100
add currency dollar
set rate dollar ruble 1:60
deposit 1 dollar
convert 80 ruble to dollar
withdraw 2.1 dollar
show balance
show total
show total in dollar
```

Вывод

20.00 ruble  
0.23 dollar  
34.00 ruble  
0.57 dollar

## Пример работы банка

```
Client <name> <surname> <passport> <subId> <currency> <amount>
```

Запуск:

```
Client Nikolay Ivanov 239239 239 ruble 100
```

Вывод (при условии запущенного сервера)

```
Creating wallet
Amount of ruble is: 0.00

Adding 100 ruble...
Amount of ruble is: 100.00
```