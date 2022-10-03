# Домашнее задание к занятию "7.5. Основы golang"

С `golang` в рамках курса, мы будем работать не много, поэтому можно использовать любой IDE.
Но рекомендуем ознакомиться с [GoLand](https://www.jetbrains.com/ru-ru/go/).

## Задача 1. Установите golang.
1. Воспользуйтесь инструкций с официального сайта: [https://golang.org/](https://golang.org/).
2. Так же для тестирования кода можно использовать песочницу: [https://play.golang.org/](https://play.golang.org/).

```bash
asm@asm-edu:~$ go version
go version go1.18.1 linux/amd64
```

## Задача 2. Знакомство с gotour.
У Golang есть обучающая интерактивная консоль [https://tour.golang.org/](https://tour.golang.org/).
Рекомендуется изучить максимальное количество примеров. В консоли уже написан необходимый код,
осталось только с ним ознакомиться и поэкспериментировать как написано в инструкции в левой части экрана.

## Задача 3. Написание кода.
Цель этого задания закрепить знания о базовом синтаксисе языка. Можно использовать редактор кода
на своем компьютере, либо использовать песочницу: [https://play.golang.org/](https://play.golang.org/).

1. Напишите программу для перевода метров в футы (1 фут = 0.3048 метр). Можно запросить исходные данные
у пользователя, а можно статически задать в коде.
    Для взаимодействия с пользователем можно использовать функцию `Scanf`:
    ```
    package main

    import "fmt"

    func main() {
        fmt.Print("Enter a number: ")
        var input float64
        fmt.Scanf("%f", &input)

        output := input * 2

        fmt.Println(output)
    }
    ```

ОТВЕТ:

```go
package main

import "fmt"

func Convert(meters float64) (result float64) {
        result = meters * 0.3048
        return result
}

func main() {
        fmt.Print("Enter a distance: ")
        var input float64
        fmt.Scanf("%f", &input)
        fmt.Printf("Distance = %v feets\n", Convert(input))
}
```

```bash
asm@asm-edu:~/netology/07-terraform-05-golang$ go run feetcalc.go
Enter a distance: 100
Distance = 30.48 feets
```

1. Напишите программу, которая найдет наименьший элемент в любом заданном списке, например:
    ```
    x := []int{48,96,86,68,57,82,63,70,37,34,83,27,19,97,9,17,}
    ```

```go
package main

import "fmt"

func getMin(array []int) (output int) {
        output = array[0]
        for _, value := range array {
                if value < output {
                        output = value
                }
        }
        return output
}

func main() {
        x := []int{48, 96, 86, 68, 57, 82, 63, 70, 37, 34, 83, 27, 19, 97, 9, 17}

        fmt.Printf("Minimal value =  %v\n", getMin(x))
}
```

```bash
asm@asm-edu:~/netology/07-terraform-05-golang$ go run minsearch.go
Minimal value =  9
```

1. Напишите программу, которая выводит числа от 1 до 100, которые делятся на 3. То есть `(3, 6, 9, …)`.

```go
package main

import (
        "fmt"
)

func devision(byNumber int) (array []int) {
        for i := 1; i <= 100; i++ {
                if i%byNumber == 0 {
                        array = append(array, i)
                }
        }
        return array
}

func main() {
        fmt.Print("Enter a number: ")
        var input int
        fmt.Scanf("%d", &input)
        for _, v := range devision(input) {
                fmt.Println(v)
        }
}
```

```bash
asm@asm-edu:~/netology/07-terraform-05-golang$ go run 3division.go
Enter a number: 3
3
6
9
12
15
18
21
24
27
30
33
36
39
42
45
48
51
54
57
60
63
66
69
72
75
78
81
84
87
90
93
96
99
```

В виде решения ссылку на код или сам код.

## Задача 4. Протестировать код (не обязательно).

Создайте тесты для функций из предыдущего задания.

---
