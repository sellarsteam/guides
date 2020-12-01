# Отчёт по C#

## Лабораторная работа 5

### Задание 1

 В консольном приложении реализовать работу с классами Parallel и Bar (материал из лекции).

#### Код

```C#
using System;

namespace ConsoleApp1
{
    class Program
    {
        class Parallel
        {
            public double a, b, c;
            public Parallel(double a, double b, double c)
            {
                this.a = a;
                this.b = b;
                this.c = c;
            }
            public double Volume()
            {
                return this.a * this.b * this.c;
            }
            public void Show()
            {
                Console.WriteLine("a = " + this.a.ToString() + "; b = " + this.b.ToString() 
                                  + "; c = " + this.c.ToString() + "; Volume = " + this.Volume().ToString());
            }
        }
        class Bar : Parallel
        {
            public double r;
            public Bar(double a, double b, double c, double r) : base(a, b, c)
            {
                this.r = r;
            }
            public double Mass()
            {
                return a * b * c * r;
            }
        }

        static void Main(string[] args)
        {
            Parallel parallel = new Parallel(3, 1, 5);
            parallel.Show();
            Bar bar = new Bar(3, 4, 6, 8);
            Console.WriteLine("Mass = " + bar.Mass().ToString());
            Console.ReadKey();
        }
    }
}
```

#### Вывод

a = 3; b = 1; c = 5; Volume = 15
Mass = 576

### Задание 2. Вариант 2

Создать класс квадрат, поле класса - длина стороны. Предусмотреть в  классе методы вычисления и вывода сведений о фигуре диагональ, периметр, площадь. Создать производный класс – правильная квадратная призма с  высотой H, добавить в класс методоопределения объема фигуры, перегрузить  методы расчета площади и вывода сведений о фигуре.

#### Код

```c#
using System;
using System.Linq;

namespace ConsoleApp2
{
    class Program
    {
        static void Main(string[] args)
        {
            Square square = new Square(2.1F);
            Console.WriteLine("Square: " + square.getDiagonal());
            Console.WriteLine("Square: " + square.getPerimeter());
            Console.WriteLine("Square: " + square.getArea());
            
            RegularSquarePrism rsp = new RegularSquarePrism(2.2F);
            Console.WriteLine("RSP: " + rsp.getVolume());
            Console.WriteLine("RSP: " + rsp.getArea());
            Console.WriteLine("RSP: " + rsp.getArea(2));
            rsp.printData();
            rsp.printData('a');
            rsp.printData('v');
            rsp.printData('n');
        }
    }

    class Square
    {
        public float line;

        public Square(float line)
        {
            this.line = line;
        }

        public float getDiagonal()
        {
            return (float)1.4 * this.line;
        }

        public float getPerimeter()
        {
            return 4 * this.line;
        }

        public float getArea()
        {
            return (float) Math.Pow(this.line, 2);
        }
    }

    class RegularSquarePrism : Square
    {
        public float line;
        public float height;

        public RegularSquarePrism(float line) : base(line)
        {
            this.line = line;
            this.height = line;
        }

        public float getVolume()
        {
            return (float) Math.Pow(this.line, 3);
        }

        public float getArea()
        {
            return (float) 12 * this.line;
        }
        
        public float getArea(int count)
        {
            return (float) 12 * this.line * count;
        }

        public void printData()
        {
            Console.WriteLine("Line is: " + this.line + "\nHeight is: " + height);
        }

        public void printData(char data)
        {
            switch (data)
            {
                case 'a':
                    Console.WriteLine("Area is: " + this.getArea());
                    break;
                case 'v':
                    Console.WriteLine("Volume is: " + this.getVolume());
                    break;
                default:
                    Console.WriteLine("Uncorrect type");
                    break;
            }
        }
    }
}
```

#### Вывод

Square: 2.9399998
Square: 8.4
Square: 4.4099994
RSP: 10.648001
RSP: 26.400002
RSP: 52.800003
Line is: 2.2
Height is: 2.2
Area is: 26.400002
Volume is: 10.648001
Uncorrect type