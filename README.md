# 12
1
#include <iostream>
#include <fstream>
#include <string> 
#include <algorithm>
#include "math.h"

using namespace std;
float arr[33] = { 8.2,1.59,4.4,1.96,2.68,7.98,0.04,1.04,1.89,6.65,1.11,3.39,5.89,3.21,6.74,10.73,2.54,4.53,5.17,4.9,
                  2.95,0.16,0.87,0.44,1.04,1.3,0.21,0.04,1.90,1.94,0.32,0.64,2.10 };
float arrn[33] = { 0 };
float arr3[33] = { 0 };
float arr4[33] = { 0 };

int sym = 1;
int symn = 0;
int i = 0;
int k = 0;
string A = "ТАПОКБВГДЕЁЖЗИЙЛМНРСУФХЦЧШЩЪЫЬЭЮЯ";
string a = "тапокбвгдеёжзийлмнрсуфхцчшщъыьэюя";

string text;
string textn;
string textbi;
string B = "АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ";
string b = "абвгдеёжзийклмнопрстуфхцчшщъыьэюя";
string c = "абвгдеёжзийклмнопрстуфхцчшщъыьэюя";
string d = "абвгдеёжзийклмнопрстуфхцчшщъыьэюя";

char temp, temp1;

int main()
{
    setlocale(LC_ALL, "Rus");
    //считывание файла в строки textn и textbi
    ifstream file;
    file.open("P:\\War_and_Peace.txt");
    if (file.is_open())
    {
        while (getline(file, text))
        {
            textn = textn + text;
        }
    }
    file.close();
    textbi = textn;
    //шифр Цезеря с выбором величины сдвига k
    //ввод k и сдвиг алфавита
    cout << "Введите ключ: ";
    cin >> k;
    
    for (int j = 0; j < k; j++)
    {
        temp = A[A.length() - 1];
        temp1 = a[a.length() - 1];
        for (int i = A.length(); i >= 1; i--) {
            A[i] = A[i - 1];
            a[i] = a[i - 1];
        }
        A[0] = temp;
        a[0] = temp1;
    }
    //шифрование текста 
    for (int i = 0; i < textn.length(); i++) {
        for (int j = 0; j < B.length(); j++) {
            if (textn[i] == B[j]) {
                textn[i] = a[j];
                break;
            }
            else if (textn[i] == b[j]) {
                textn[i] = a[j];
                break;
            }
        }

    }
    text = textn;
    //вывод шифрованных алфовитов и текста
    cout << "Шифрованный текст: " << endl;
    cout << textn << endl;


    //монограммный анализ
    // подсчёт количества букв
    for (int i = 0; i <= textn.length(); i++) {
        if (textn[i] != ' ' && textn[i] != 'A-Z' && textn[i] != '.' && textn[i] != ',' && textn[i] != ':' && textn[i] != '!' && textn[i] != '?' && textn[i] != '-')
            sym++;
    }

    
    //вычисление частоты появления каждой буквы
    for (int i = 0; i < textn.length(); i++) {
        for (int j = 0; j < B.length(); j++) {
            if (textn[i] == B[j] || textn[i] == b[j]) {
                arrn[j]++;
            }

        }
    }


    for (int i = 0; i < 33; i++) {
        arr3[i] = arrn[i];
    }
    sort(arrn, arrn + 33, greater<float>());
    for (int i = 0; i < 33; i++) {
        for (int j = 0; j < 33; j++) {
            if (arr3[i] == arrn[j]) {
                c[j] = b[i];
                break;
            }

        }
    }
    for (int i = 0; i < 33; i++) {
        arr4[i] = arr[i];
    }
    
    sort(arr, arr + 33, greater<float>());
    for (int i = 0; i < 33; i++) {
        for (int j = 0; j < 33; j++) {
            if (arr4[i] == arr[j]) {
                d[j] = b[i];
                break;
            }

        }
    }
    for (int i = 0; i < textn.length(); i++) {
        for (int j = 0; j < B.length(); j++) {
            if (textn[i] == c[j]) {
                textn[i] = d[j];
                break;
            }

        }

    }
    cout << "\n\nДешифрация монограммами: " << endl;
    cout << textn << endl;
    
    system("pause");
}
