1 Задание
using System;

class Program
{
    // Быстрое вычисление факториала через цикл
    static double Factorial(int n)
    {
        double res = 1;
        for (int i = 2; i <= n; i++) res *= i;
        return res;
    }

    // Вычисление n-го члена ряда Маклорена (пример для e^x)
    static double NthTerm(double x, int n) => Math.Pow(x, n) / Factorial(n);

    // Сумма ряда с заданной точностью
    static double Series(double x, double eps)
    {
        double sum = 1, term = 1; // начинаем с n=0, член равен 1
        for (int n = 1; Math.Abs(term) > eps; n++)
        {
            term = NthTerm(x, n);
            sum += term;
        }
        return sum;
    }

    static void Main()
    {
        Console.Write("Введите x: ");
        double x = double.Parse(Console.ReadLine()!);

        Console.Write("Введите точность (e < 0.01): ");
        double eps = double.Parse(Console.ReadLine()!);

        if (eps >= 0.01) { Console.WriteLine("Ошибка: e должно быть < 0.01"); return; }

        Console.WriteLine($"f(x) ≈ {Series(x, eps):F6}");

        Console.Write("Введите номер члена n: ");
        int n = int.Parse(Console.ReadLine()!);
        Console.WriteLine($"{n}-й член ряда = {NthTerm(x, n):F6}");
    }
}

Вывод : Введите x: 12
Введите точность (e < 0.01): 0,0001
f(x) ? 162754,791394
Введите номер члена n: 23
23-й член ряда = 256,256111

Задание 2
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите шестизначный номер билета: ");
        if (!int.TryParse(Console.ReadLine(), out int num) || num < 0 || num > 999999)
        {
            Console.WriteLine("Ошибка: нужно ввести 6-значное число.");
            return;
        }

        // Извлекаем цифры вручную, без строк и массивов
        int sum1 = 0, sum2 = 0;
        for (int i = 0; i < 3; i++)
        {
            sum1 += num % 10;  // последние 3 цифры
            num /= 10;
        }
        for (int i = 0; i < 3; i++)
        {
            sum2 += num % 10;  // первые 3 цифры
            num /= 10;
        }

        Console.WriteLine(sum1 == sum2 ? "Билет счастливый!" : "Билет обычный.");
    }
}
Вывод : 
Введите шестизначный номер билета: 123456
Билет обычный.

Задание 3
using System;

class Program
{
    // Быстрый НОД (алгоритм Евклида)
    static int GCD(int a, int b) => b == 0 ? Math.Abs(a) : GCD(b, a % b);

    static void Main()
    {
        Console.Write("Введите M: ");
        int m = int.Parse(Console.ReadLine()!);
        Console.Write("Введите N: ");
        int n = int.Parse(Console.ReadLine()!);

        if (n == 0) { Console.WriteLine("Ошибка: знаменатель не может быть 0."); return; }

        int d = GCD(m, n);
        Console.WriteLine($"Несократимая дробь: {m / d}/{n / d}");
    }
}
Вывод :
Введите M: 12
Введите N: 12
Несократимая дробь: 1/1

4 Задание
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Загадайте число от 0 до 63.");
        int result = 0;

        // Проходим по каждому из 6 бит числа
        for (int i = 0; i < 6; i++)
        {
            int value = 1 << i; // проверяем бит
            Console.Write($"Ваше число >= {value}? (1/0): ");
            if (Console.ReadLine() == "1") result |= value;
        }

        Console.WriteLine($"Ваше число: {result}");
    }
}
Вывод :
Загадайте число от 0 до 63.
Ваше число >= 1? (1/0): 1
Ваше число >= 2? (1/0): 1
Ваше число >= 4? (1/0): 1
Ваше число >= 8? (1/0): 1
Ваше число >= 16? (1/0): 0
Ваше число >= 32? (1/0): 0
Ваше число: 15

5 Задание
using System;

class Program
{
    const int AM_WATER = 300, LAT_WATER = 30, LAT_MILK = 270;
    const int AM_PRICE = 150, LAT_PRICE = 170;

    static void Main()
    {
        Console.Write("Воды (мл): ");
        int water = int.Parse(Console.ReadLine()!);
        Console.Write("Молока (мл): ");
        int milk = int.Parse(Console.ReadLine()!);

        int amCount = 0, latCount = 0, profit = 0;

        while (true)
        {
            // Проверяем, можно ли вообще что-то приготовить
            if (water < LAT_WATER && water < AM_WATER || milk < LAT_MILK && water < AM_WATER)
                break;

            Console.Write("\nВыберите напиток (1-Американо, 2-Латте): ");
            string choice = Console.ReadLine()!;
            switch (choice)
            {
                case "1" when water >= AM_WATER:
                    water -= AM_WATER; amCount++; profit += AM_PRICE;
                    Console.WriteLine("Ваш американо готов!");
                    break;
                case "2" when water >= LAT_WATER && milk >= LAT_MILK:
                    water -= LAT_WATER; milk -= LAT_MILK; latCount++; profit += LAT_PRICE;
                    Console.WriteLine("Ваш латте готов!");
                    break;
                default:
                    Console.WriteLine("Недостаточно ингредиентов!");
                    break;
            }
        }

        Console.WriteLine($"\nИнгредиенты закончились.\nОстаток: вода={water} мл, молоко={milk} мл.");
        Console.WriteLine($"Продано: американо={amCount}, латте={latCount}, заработано={profit} руб.");
    }
}
Вывод : 
Воды (мл): 250
Молока (мл): 200

Ингредиенты закончились.
Остаток: вода=250 мл, молоко=200 мл.
Продано: американо=0, латте=0, заработано=0 руб.

Задание 6
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите N (бактерий): ");
        int n = int.Parse(Console.ReadLine()!);
        Console.Write("Введите X (капель антибиотика): ");
        int x = int.Parse(Console.ReadLine()!);

        int hour = 0, kill = x * 10;

        while (n > 0 && kill > 0)
        {
            hour++;
            n *= 2;       // бактерии удваиваются
            n -= kill;    // антибиотик убивает
            if (n < 0) n = 0;
            kill -= x;    // эффективность падает

            Console.WriteLine($"Час {hour}: бактерий = {n}, сила антибиотика = {kill}");
        }

        Console.WriteLine($"\nПроцесс завершён за {hour} часов. Осталось бактерий: {n}");
    }
}

Вывод : 
Введите N (бактерий): 12
Введите X (капель антибиотика): 23
Час 1: бактерий = 0, сила антибиотика = 207

Процесс завершён за 1 часов. Осталось бактерий: 0

Задание 7
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите количество модулей (n): ");
        if (!int.TryParse(Console.ReadLine(), out int n) || n <= 0)
        {
            Console.WriteLine("Ошибка: нужно ввести положительное число модулей.");
            return;
        }

        Console.Write("Введите размеры модуля (a b): ");
        var ab = Console.ReadLine()!.Split(' ', StringSplitOptions.RemoveEmptyEntries);
        if (ab.Length < 2 || !int.TryParse(ab[0], out int a) || !int.TryParse(ab[1], out int b))
        {
            Console.WriteLine("Ошибка: нужно ввести два числа (a и b).");
            return;
        }

        Console.Write("Введите размеры поля (h w): ");
        var hw = Console.ReadLine()!.Split(' ', StringSplitOptions.RemoveEmptyEntries);
        if (hw.Length < 2 || !int.TryParse(hw[0], out int h) || !int.TryParse(hw[1], out int w))
        {
            Console.WriteLine("Ошибка: нужно ввести два числа (h и w).");
            return;
        }

        int result = MaxD(n, a, b, h, w);
        Console.WriteLine(result == -1
            ? "Размещение невозможно даже без защиты."
            : $"Максимальная толщина защиты: {result}");
    }

    // Бинарный поиск максимальной толщины d
    static int MaxD(int n, int a, int b, int h, int w)
    {
        if (!CanPlace(n, a, b, h, w, 0)) return -1;

        int left = 0, right = Math.Min(h, w) / 2, best = 0;

        while (left <= right)
        {
            int mid = (left + right) / 2;
            if (CanPlace(n, a, b, h, w, mid))
            {
                best = mid;       // нашли подходящее значение
                left = mid + 1;   // пробуем больше
            }
            else right = mid - 1;
        }

        return best;
    }

    // Проверяем, можно ли разместить модули с толщиной защиты d
    static bool CanPlace(int n, int a, int b, int h, int w, int d)
    {
        int A = a + 2 * d, B = b + 2 * d;
        return Fit(n, A, B, h, w) || Fit(n, B, A, h, w);
    }

    // Проверяем, влезут ли все модули на поле (ориентация фиксирована)
    static bool Fit(int n, int a, int b, int h, int w)
    {
        int rows = h / a, cols = w / b;
        return rows * cols >= n;
    }
}
Вывод :
Введите количество модулей (n): 12
Введите размеры модуля (a b): 2 3
Введите размеры поля (h w): 2 5
Размещение невозможно даже без защиты.
