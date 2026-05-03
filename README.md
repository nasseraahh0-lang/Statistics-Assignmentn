namespace Tast_1
{
    internal class Program
    {
        static double Mean(int[] Numbers)
        {
            double sum = 0;
            double Mean = 0;
            for (int i = 0; i < Numbers.Length; i++)
            {
                sum += Numbers[i];
            }
            Mean = sum / Numbers.Length;
            return Mean;
        }
        static int Mode(int[] Numbers)
        {   
            int Count = 0;
            int MaxCount = 0;
            int intex = 0;
            for (int i = 0; i < Numbers.Length; i++)
            {
                Count = 0;
                for (int j = i + 1; j < Numbers.Length; j++)
                {
                    if (Numbers[i] == Numbers[j])
                        Count++;
                }
                if (Count > MaxCount)
                {
                    MaxCount = Count;
                    intex = i;
                }
            }
            return Numbers[intex];
        }
        static int Median(int[] Numbers)
        {
            Array.Sort(Numbers);
            return Numbers[Numbers.Length / 2];
        }
        static double Var(int[] Numbers)
        {
            double sum = 0;
            double num = Mean(Numbers);
            for (int i = 0; i < Numbers.Length; i++)
            {
                sum += (Numbers[i] - num) * (Numbers[i] - num);
            }
            double Variance = sum / Numbers.Length;
            return Variance;
        }
        static double Percentile(int[] Numbers, double num)
        {
            Array.Sort(Numbers);
            double rank = (num / 100) * (Numbers.Length + 1);
            int rank_integar = Convert.ToInt32(rank);
            double Percentile = 0;
            if (rank_integar == rank)
                Percentile = Numbers[rank_integar - 1];
            else
                Percentile = Numbers[rank_integar - 1] + (Numbers[rank_integar] - Numbers[rank_integar - 1]) * (rank - rank_integar);

            return Percentile;
        }
        static double Quartile(int[] Numbers, int num)
        {
            Array.Sort(Numbers);
            double rank = num * (Numbers.Length + 1) / 4.0;
            int rank_integar = Convert.ToInt32(rank);
            double Quartile = 0;
            if (rank_integar == rank)
                Quartile = Numbers[rank_integar - 1]; 
            else
                Quartile = Numbers[rank_integar - 1] + (Numbers[rank_integar] - Numbers[rank_integar - 1]) * (rank - rank_integar);
            return rank;
        }
        static int Range(int[] Numbers)
        {
            Array.Sort(Numbers);
            return (Numbers[Numbers.Length - 1] - Numbers[0]);
        }
        static double IQR(int[] Numbers)
        {
            return (Quartile(Numbers, 3) - Quartile(Numbers, 1));
        }
        static double SD(int[] Numbers)
        {
            return Math.Sqrt(Var(Numbers));
        }
        static double SummtionOfDivision(int[] Numbers)
        {
            double sum = 0;
            foreach (int i in Numbers) { sum += i; }
            return sum - (Numbers.Length * Mean(Numbers));
        }
        static void Main(string[] args)
        {
            int[] Numbers = new int[]
            {
                115, 182, 191, 31, 196,1099, 
                5, 172, 10, 179, 83, 21,20, 
                21, 186, 177, 195, 193, 188,
                199, 62, 109, 105, 183, 110
            };
            Console.WriteLine($"Mean:{Mean(Numbers)}");
            Console.WriteLine($"Mode:{Mode(Numbers)}");
            Console.WriteLine($"Median:{Median(Numbers)}");
            Console.WriteLine($"Var:{Var(Numbers)}");
            Console.WriteLine($"P20:{Percentile(Numbers, 20)}");
            Console.WriteLine($"P50:{Percentile(Numbers, 50)}");
            Console.WriteLine($"Q1:{Quartile(Numbers, 1)}");
            Console.WriteLine($"Q2:{Quartile(Numbers, 2)}");
            Console.WriteLine($"Q3:{Quartile(Numbers, 3)}");
            Console.WriteLine($"R:{Range(Numbers)}");
            Console.WriteLine($"IQR:{IQR(Numbers)}");
            Console.WriteLine($"SD:{SD(Numbers)}");
            Console.WriteLine($"Summation of Divisions:{SummtionOfDivision(Numbers)}");
        }
    }
