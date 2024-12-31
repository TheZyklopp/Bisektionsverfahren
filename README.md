# Bisektionsverfahren
```csharp
using System;

namespace Bisektionsverfahren
{
    class Program
    {
        public static double ContinuousFunction(double x)
        {
            return Math.Pow(x, 3) + x - 5;
        }

        public static double CalculateRootOfPolynomial(double a, double b)
        {
            if (a >= b || Math.Sign(ContinuousFunction(a)) == Math.Sign(ContinuousFunction(b)))
            {
                return double.NaN;
            }

            double mid = 0;
            int iterations = 0;
            const double tolerance = 1e-6;
            const int maxIterations = 1000;

            while ((b - a) >= tolerance && iterations < maxIterations)
            {
                mid = (a + b) / 2;
                double fMid = ContinuousFunction(mid);

                if (Math.Abs(fMid) < tolerance)
                {
                    break;
                }

                if (Math.Sign(fMid) == Math.Sign(ContinuousFunction(a)))
                {
                    a = mid;
                }
                else
                {
                    b = mid;
                }

                iterations++;
            }

            return mid;
        }

        static void Main(string[] args)
        {
            Console.WriteLine("Test der Funktion ContinuousFunction:");
            Console.WriteLine($"f(2) = {ContinuousFunction(2)}");

            Console.WriteLine("\nTest des Bisektionsverfahrens:");

            double root = CalculateRootOfPolynomial(1, 2);
            if (double.IsNaN(root))
            {
                Console.WriteLine("Keine gültige Nullstelle im angegebenen Intervall gefunden.");
            }
            else
            {
                Console.WriteLine($"Die berechnete Nullstelle ist: {root}");
            }

            Console.WriteLine("\nWeitere Tests mit Spezialfällen:");

            double invalidRoot = CalculateRootOfPolynomial(2, 1);
            Console.WriteLine($"Test mit a > b: {invalidRoot}");

            double invalidSigns = CalculateRootOfPolynomial(1, 1.5);
            Console.WriteLine($"Test mit gleichen Vorzeichen an den Intervallgrenzen: {invalidSigns}");
        }
    }
}
