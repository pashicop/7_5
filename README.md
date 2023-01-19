# 7_5
## Задача 1. Установите golang.
Установил Goland и GO 1.19.5  
![go version](https://user-images.githubusercontent.com/97126500/213318540-732ceae6-d93a-45b1-9891-e919fcf9c9a6.png)
## Задача 2. Знакомство с gotour.
Ознакомился с основными примерами на gotour
## Задача 3. Написание кода.
### 1.
Написал дополнительную функцию get_foots() перевода метры в футы
```
package main

import "fmt"

func get_foots(m float64) float64 {
	return (m / 0.3048)
}

func main() {
	var input float64
	fmt.Printf("Введите метры: \n")
	fmt.Scanf("%f", &input)
	output := get_foots(input)
	fmt.Printf("Получаем в футах - %.2f\n", output)
}
```
Пример использования:
```
Введите метры:
10
Получаем в футах - 32.81

Process finished with the exit code 0
```
### 2.
Вычисляю методом пузырька наименьшее значение массива
```
package main

import "fmt"

func getMin(mas []int) int {
	var min int = mas[0]
	for i := 0; i < len(mas)-1; i++ {
		if min > mas[i+1] {
			min = mas[i+1]
		}
	}
	return min
}

func main() {
	x := []int{48, 96, 86, 68, 57, 82, 63, 70, 37, 34, 83, 27, 19, 97, 9, 17}
	fmt.Printf("Минимальное значение = %v", getMin(x))
}
```
Вывод:
```
C:\Users\shitikov\AppData\Local\Temp\GoLand\___go_build_awesomeProject.exe
Минимальное значение = 9
Process finished with the exit code 0
```
### 3.
Написал функцию проверки деления на 3. Также вывожу количество таких чисел
```
package main

import "fmt"

func getMasDivByThree() []int {
	var sum = 0
	for i := 1; i < 100; i++ {
		if i%3 == 0 {
			fmt.Printf("%v ", i)
			sum++
		}
	}
	fmt.Printf("\nВсего таких чисел: %v", sum)
	return nil
}

func main() {
	fmt.Println("Числа от 1 до 100, делящиеся на 3")
	getMasDivByThree()
}
```
Вывод:
```
C:\Users\shitikov\AppData\Local\Temp\GoLand\___go_build_awesomeProject.exe
Числа от 1 до 100, делящиеся на 3
3 6 9 12 15 18 21 24 27 30 33 36 39 42 45 48 51 54 57 60 63 66 69 72 75 78 81 84
 87 90 93 96 99
Всего таких чисел: 33
Process finished with the exit code 0
```
## Задача 4
Поэксперементировал с простыми тестами, чтобы посмотреть принцип написания тестов. Вот пример:
```
package main

import (
	"fmt"
	"testing"
)

func TestGetMinTableDriven(t *testing.T) {
	var tests = []struct {
		x    []int
		want int
	}{
		{[]int{0, 1, 5}, 0},
		{[]int{0, 1, 6}, 1},
		{[]int{0, 5, 6}, 0},
		{[]int{0, 1, 89}, 0},
	}
	for _, tt := range tests {
		testname := fmt.Sprintf("%d", tt.x)
		t.Run(testname, func(t *testing.T) {
			ans := getMin(tt.x)
			if ans != tt.want {
				t.Errorf("got %d, want %d", ans, tt.want)
			}
		})
	}
}
```
В тесте специально сделал ошибку, чтобы посмотреть вывод:
```
"C:\Program Files\Go\bin\go.exe" tool test2json -t C:\Users\shitikov\AppData\Local\Temp\GoLand\___TestGetMinTableDriven_in_awesomeProject.test.exe -test.v -test.paniconexit0 -test.run ^\QTestGetMinTableDriven\E$ #gosetup
=== RUN   TestGetMinTableDriven
--- FAIL: TestGetMinTableDriven (0.00s)
=== RUN   TestGetMinTableDriven/[0_1_5]
    --- PASS: TestGetMinTableDriven/[0_1_5] (0.00s)
=== RUN   TestGetMinTableDriven/[0_1_6]
    main_test.go:23: got 0, want 1
    --- FAIL: TestGetMinTableDriven/[0_1_6] (0.00s)

=== RUN   TestGetMinTableDriven/[0_5_6]
    --- PASS: TestGetMinTableDriven/[0_5_6] (0.00s)
=== RUN   TestGetMinTableDriven/[0_1_89]
    --- PASS: TestGetMinTableDriven/[0_1_89] (0.00s)

FAIL


Process finished with the exit code 1
```
