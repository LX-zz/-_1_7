# 💻 Программирование корпоративных систем — Рабочая тетрадь №2  
## 🔁 Циклы и базовые алгоритмы на C#

```csharp


    // 🧮 Задание 1 — Ряды (разложение функции через ряд Маклорена)
    static void Task1()
    {
        double Factorial(int n)
        {
            double res = 1;
            for (int i = 2; i <= n; i++) res *= i;
            return res;
        }

        double NthTerm(double x, int n) => Math.Pow(x, n) / Factorial(n);

        double Series(double x, double eps)
        {
            double sum = 1, term = 1;
            for (int n = 1; Math.Abs(term) > eps; n++)
            {
                term = NthTerm(x, n);
                sum += term;
            }
            return sum;
        }

        Console.Write("Введите x: ");
        double x = double.Parse(Console.ReadLine()!);

        Console.Write("Введите точность (e < 0.01): ");
        double eps = double.Parse(Console.ReadLine()!);

        if (eps >= 0.01)
        {
            Console.WriteLine("Ошибка: e должно быть < 0.01");
            return;
        }

        Console.WriteLine($"f(x) ≈ {Series(x, eps):F6}");
        Console.Write("Введите номер члена n: ");
        int n = int.Parse(Console.ReadLine()!);
        Console.WriteLine($"{n}-й член ряда = {NthTerm(x, n):F6}");
    }

    // 🎟 Задание 2 — Счастливый билет
    static void Task2()
    {
        Console.Write("Введите шестизначный номер билета: ");
        if (!int.TryParse(Console.ReadLine(), out int num) || num < 0 || num > 999999)
        {
            Console.WriteLine("Ошибка: нужно ввести 6-значное число.");
            return;
        }

        int sum1 = 0, sum2 = 0;
        for (int i = 0; i < 3; i++) { sum1 += num % 10; num /= 10; }
        for (int i = 0; i < 3; i++) { sum2 += num % 10; num /= 10; }

        Console.WriteLine(sum1 == sum2 ? "Билет счастливый!" : "Билет обычный.");
    }

    // ➗ Задание 3 — Сокращение дроби
    static void Task3()
    {
        int GCD(int a, int b) => b == 0 ? Math.Abs(a) : GCD(b, a % b);

        Console.Write("Введите M: ");
        int m = int.Parse(Console.ReadLine()!);
        Console.Write("Введите N: ");
        int n = int.Parse(Console.ReadLine()!);

        if (n == 0)
        {
            Console.WriteLine("Ошибка: знаменатель не может быть 0.");
            return;
        }

        int d = GCD(m, n);
        Console.WriteLine($"Несократимая дробь: {m / d}/{n / d}");
    }

    // 🔢 Задание 4 — Угадай число
    static void Task4()
    {
        Console.WriteLine("Загадайте число от 0 до 63.");
        int result = 0;

        for (int i = 0; i < 6; i++)
        {
            int value = 1 << i;
            Console.Write($"Ваше число >= {value}? (1/0): ");
            if (Console.ReadLine() == "1") result |= value;
        }

        Console.WriteLine($"Ваше число: {result}");
    }

    // ☕ Задание 5 — Кофейный аппарат
    static void Task5()
    {
        const int AM_WATER = 300, LAT_WATER = 30, LAT_MILK = 270;
        const int AM_PRICE = 150, LAT_PRICE = 170;

        Console.Write("Воды (мл): ");
        int water = int.Parse(Console.ReadLine()!);
        Console.Write("Молока (мл): ");
        int milk = int.Parse(Console.ReadLine()!);

        int amCount = 0, latCount = 0, profit = 0;

        while (true)
        {
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

        Console.WriteLine($"\nИнгредиенты закончились.");
        Console.WriteLine($"Остаток: вода={water} мл, молоко={milk} мл.");
        Console.WriteLine($"Продано: американо={amCount}, латте={latCount}, заработано={profit} руб.");
    }

    // 🧫 Задание 6 — Лабораторный опыт
    static void Task6()
    {
        Console.Write("Введите N (бактерий): ");
        int n = int.Parse(Console.ReadLine()!);
        Console.Write("Введите X (капель антибиотика): ");
        int x = int.Parse(Console.ReadLine()!);

        int hour = 0, kill = x * 10;

        while (n > 0 && kill > 0)
        {
            hour++;
            n *= 2;
            n -= kill;
            if (n < 0) n = 0;
            kill -= x;
            Console.WriteLine($"Час {hour}: бактерий = {n}, сила антибиотика = {kill}");
        }

        Console.WriteLine($"\nПроцесс завершён за {hour} часов. Осталось бактерий: {n}");
    }

    // 🚀 Задание 7 — Колонизация Марса
    static void Task7()
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

    static int MaxD(int n, int a, int b, int h, int w)
    {
        if (!CanPlace(n, a, b, h, w, 0)) return -1;

        int left = 0, right = Math.Min(h, w) / 2, best = 0;

        while (left <= right)
        {
            int mid = (left + right) / 2;
            if (CanPlace(n, a, b, h, w, mid))
            {
                best = mid;
                left = mid + 1;
            }
            else right = mid - 1;
        }
        return best;
    }

    static bool CanPlace(int n, int a, int b, int h, int w, int d)
    {
        int A = a + 2 * d, B = b + 2 * d;
        return Fit(n, A, B, h, w) || Fit(n, B, A, h, w);
    }

    static bool Fit(int n, int a, int b, int h, int w)
    {
        int rows = h / a, cols = w / b;
        return rows * cols >= n;
    }
}
