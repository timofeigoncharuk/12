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
  
  
  2лаба
  #include <iostream>
#include <string>
#include <cmath>
#include <cstring>
#include <cstdlib>
#include <time.h>
#include <cstdlib>
#define ll long long
using namespace std;
ll int A_public = 0;
ll int A_private = 0;
ll int B_public = 0;
ll int B_private = 0;
string message = "Полевая ромашка!";
string enc_message = "";
string dec_message = "";
ll int A_partial = 0;
ll int B_partial = 0;
ll int A_full = 0;
ll int B_full = 0;
ll mulmod(ll a, ll b, ll mod)
{
    ll x = 0, y = a % mod;
    while (b > 0)
    {
        if (b % 2 == 1)
        {
            x = (x + y) % mod;
        }
        y = (y * 2) % mod;
        b /= 2;
    }
    return x % mod;
}

ll modulo(ll base, ll exponent, ll mod)
{
    ll x = 1;
    ll y = base;
    while (exponent > 0)
    {
        if (exponent % 2 == 1)
            x = (x * y) % mod;
        y = (y * y) % mod;
        exponent = exponent / 2;
    }
    return x % mod;
}


bool Miller(ll int p, int iteration)
{
    if (p < 2)
    {
        return false;
    }
    if (p != 2 && p % 2 == 0)
    {
        return false;
    }
    ll s = p - 1;
    while (s % 2 == 0)
    {
        s /= 2;
    }
    for (int i = 0; i < iteration; i++)
    {
        ll a = rand() % (p - 1) + 1, temp = s;
        ll mod = modulo(a, temp, p);
        while (temp != p - 1 && mod != 1 && mod != p - 1)
        {
            mod = mulmod(mod, mod, p);
            temp *= 2;
        }
        if (mod != p - 1 && temp % 2 == 0)
        {
            return false;
        }
    }
    return true;
}
int Generator() {
    int iteration = 5;
    ll num;
    num = rand()%20+2;
    Miller(num, iteration);
    if (Miller(num, iteration))
        return num;
    else Generator();
}
int partial_key(int public_1, int private_1, int public_2) {
    int partial = pow(public_1, private_1);
    partial %= public_2;
    return partial;
}
int main()
{
    srand(time(NULL));
    setlocale(LC_ALL, "rus");
    //A_public = Generator();
    //A_private = Generator();
    //B_public = Generator();
    //B_private = Generator();
    cout << message << endl;
    A_public = 13;
    A_private = 7;
    B_public = 11;
    B_private = 3;
    cout <<"A_public: " << A_public << endl;
    cout <<"A_private: "<< A_private << endl;
    cout << "B_public: " << B_public << endl;
    cout << "B_private: " << B_private << endl;
    A_partial = pow(A_public, A_private);
    cout << "Промежуточный A_p: " << A_partial << endl;
    A_partial = A_partial % B_public;
    cout << A_partial << endl;
    B_partial = pow(A_public, B_private);
    cout <<"Промежуточный B_p: " << B_partial << endl;
    B_partial = B_partial % B_public;
    cout << B_partial << endl;
    A_full = pow(B_partial, A_private);
    cout << "Промежуточный A_F : " << A_full << endl;
    A_full = A_full % B_public;
    cout << A_full<<endl;
    B_full = pow(A_partial, B_private);
    cout << "Промежуточный B_F : " << B_full << endl;
    B_full = B_full % B_public;
    cout << B_full<<endl;
    enc_message = "";
    for (int i = 0; i < message.length(); i++) {
        enc_message += char((int)(message[i] + A_full));
    }
    cout << enc_message << endl;
    dec_message = "";
    for (int i = 0; i < enc_message.length(); i++) {
        
        dec_message += char((int)(enc_message[i] - B_full));
    }
    cout << dec_message << endl;
    return 0;
}
