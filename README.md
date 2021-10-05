# Отчёт о тестировании Credit Card Number Validator

## Краткое описание

04.10.2021 - 05.10.2021 было проведено функциональное (модульное) тестирование программы Credit Card Number Validator.

На тестирование затрачено: 4 часа.

В результате тестирования выявлены следующие дефекты:
* [Не принимаются любые валидные карты, которые состоят не из 16 символов](https://github.com/aremarss/java_1.1/issues/1)

## Описание процесса тестирования

В качестве тестовых данных использовались данные [Задания 2 - Credit Card Number Validator](https://github.com/netology-code/javaqa-homeworks/blob/master/intro/MERGED.md):
___
* [Пример валидных карт из freeformatter.com](https://www.freeformatter.com/credit-card-number-generator-validator.html)
___
* Программа:
``` java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```
___
Тестирование производилось в следующем окружении:
* Windows 10, 64-bit;
* Java 11.0.12;
* IntelliJ IDEA 2021.2.2 (Community Edition).