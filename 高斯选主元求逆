using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MathNet.Numerics.LinearAlgebra;
using MathNet.Numerics.LinearAlgebra.Double;

namespace 高斯选主元求逆
{
    class Program
    {
        static void Main(string[] args)
        {
            Matrix<double> m1 = Matrix<double>.Build.Dense(3, 3);
            Matrix<double> m2 = Matrix<double>.Build.Dense(3, 3);

            //m1赋值
            m1[0, 0] = 1;
            m1[0, 1] = 3;
            m1[0, 2] = 1;
            m1[1, 0] = 2;
            m1[1, 1] = 1;
            m1[1, 2] = 1;
            m1[2, 0] = 2;
            m1[2, 1] = 2;
            m1[2, 2] = 1;

            //m2赋值
            for (int i = 0; i < 3; i++)
            {
                for (int j = 0; j < 3; j++)
                {
                    if (i == j)
                        m2[i, j] = 1;
                }
            }

            Matrix<double> m3 = m1.Inverse();
            for (int i = 0; i < 3; i++)
            {
                for (int j = 0; j < 3; j++)
                {
                    if (Math.Abs(m3[i, j]) < 10e-15)
                        m3[i, j] = 0;
                }
            }
            //Console.WriteLine(m3);

            //Vector<double> v1=Vector<double>.Build.Dense(3);
            //v1[0]=2;
            //v1[1]=3;
            //v1[2]=4;
            //m3.SetRow(1, v1);
            //Console.WriteLine(m3);


            //（列，列）
            int row = 0, col = 0;
            find_mian_element(out row, out col, m1);

            if (row != col)  //换主元
            //第row行跟第col行调换！
            {
                exchange_row(row, col, m1, m2);
            }
            change_to_0(col, m1, m2);
            Console.WriteLine(m1);
            Console.WriteLine(m2);
            //并将该列其他值化为0


            find_mian_element(out row, out col, m1);

            if (row != col)  //换主元
            //第row行跟第col行调换！
            {
                exchange_row(row, col, m1, m2);
            }
            change_to_0(col, m1, m2);
            Console.WriteLine(m1);
            Console.WriteLine(m2);

        }

        static double find_mian_element(out int row, out int col, Matrix<double> m1)
        {
            //处理过的列不参与选主元！！！
            //就是选出主元的行col不参与选主元！！！
            double max = 0;
            row = 0;
            col = 0;
            for (int i = 0; i < 3; i++)
            {
                for (int j = 0; j < 3; j++)
                {
                    if (m1[i, j] > max)
                    {
                        max = m1[i, j];
                        row = i;
                        col = j;
                    }
                }
            }
            return max;
        }


        static void exchange_row(int i1, int i2, Matrix<double> m1, Matrix<double> m2)
        {
            Vector<double> v1 = Vector<double>.Build.Dense(m1.ColumnCount);
            Vector<double> v2 = Vector<double>.Build.Dense(m1.ColumnCount);
            for (int j = 0; j < 3; j++)
            {
                v1[j] = m1[i1, j];
                m1[i1, j] = m1[i2, j];
                m1[i2, j] = v1[j];

                v2[j] = m2[i1, j];
                m2[i1, j] = m2[i2, j];
                m2[i2, j] = v2[j];

            }
        }

        static void change_to_0(int col, Matrix<double> m1, Matrix<double> m2)
        {
            double t = m1[col, col];
            for (int j = 0; j < 3; j++)
            {
                m1[col, j] /= t;
                m2[col, j] /= t;
            }

            double[] r = new double[3];
            for (int i = 0; i < 3; i++)
            {
                if (i != col)
                {
                    r[i] = m1[i, col] / m1[col, col];
                }
            }

            for (int i = 0; i < 3; i++)
            {
                for (int j = 0; j < 3; j++)
                {
                    if (i != col)
                    {
                        m1[i, j] = m1[i, j] - m1[col, j] * r[i];
                        m2[i, j] = m2[i, j] - m2[col, j] * r[i];
                    }
                }
            }


        }
    }
}
