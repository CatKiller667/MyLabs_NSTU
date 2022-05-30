// Юсупов Данил АТ-93
// Программа принимает на вход значения сигнала, на выход выводит сигнал после фильтра

#include <iostream>
#include <fstream>
#include <string>
#include <cmath>
#include <vector>
#include <ctime>
const float pi = 3.14159;
const int length_of_scalar = 1000;
using namespace std;

int main()
{
    setlocale(LC_ALL, "Russian");
    // Ввод коэффициентов
    string input; bool ak_or_bk = false;
    int a_num = 0, b_num = 0;
    float a[50], b[50];
    ifstream in("D:\\Koef tf.txt");
    if (in.is_open())
    {
        while (getline(in, input))
        {
            if (input == "Numerator:")
                ak_or_bk = true;
            else if (input == "Denominator:")
                ak_or_bk = false;
            else if (ak_or_bk == true)
            {
                a[a_num] = stof(input);
                ++a_num;
            }
            else if (ak_or_bk == false)
            {
                b[b_num] = stof(input);
                ++b_num;
            }
        }
    }
    in.close();
    //Вывод коэффициентов в консоль
    /*for (int i = 0; i < a_num; ++i)
    {
        cout << i << ") "<< a[i] << " / " << b[i] << endl;
    }*/

    //Создание входного сигнала
    
    float x[length_of_scalar] = {};
    float y[length_of_scalar] = {};
    float w = 2 * pi * 1300;
    float A = 10;
    float Fs = 5000;
    float bs, as;
    int P, Q;
    for (int n = 0; n < length_of_scalar; ++n)
        x[n] = A * sin(w * (n / Fs));

    //Прохождение сигнала через фильтр
    float start_time = clock();
    for (int rep = 0; rep < 10000; ++rep)
    {
        for (int n = 0; n < length_of_scalar; ++n)
        {
            as = 0; bs = 0;
            if (n < a_num)
                P = n;
            if (n < b_num)
                Q = n;
            for (int i = 0; i < P; ++i)
            {
                bs += b[i] * x[n - i];
            }
            for (int k = 0; k < Q; ++k)
            {
                as += a[k] * y[n - k];
            }
            y[n] = bs - as;
        }
    }
    float end_time = clock();
    float search_time = (end_time - start_time) / CLK_TCK;
    search_time = search_time / 10000;
    cout << "Время начала работы: " << start_time << endl;
    cout << "Время конца работы: " << end_time << endl;
    cout << "Время работы программы: " << search_time << endl;
    cout << __cplusplus << endl;

    /*for (int n = 0; n < length_of_scalar; ++n)
    {
        cout << y[n] << endl;
    }*/
    return 0;
}
