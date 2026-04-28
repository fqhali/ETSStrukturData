# ETSStrukturData

## 1. Jelaskan struktur data Array. Digunakan untuk apa Array, Berikan contoh penggunaanya dalam aplikasi.
Jawaban:
<br>
Array adalah salah satu dari struktur data berkategori linear, array adalah suatu variabel yang dimana array dipakai untuk menyimpan banyak data dalam satu variabelnya dengan catatan bahwa semua data tersebut bertipe data yang sama, seperti penggunaan peti yang menyimpan banyak barang dalam satu wadah. Array memiliki index yang dimana fungsi dari index tersebut adalah untuk mengakses elemen yang tersimpan dalam array yang kemudian kita panggil untuk kita olah lagi atau kita print, index array dimulai dari 0. Penggunaan dari array sendiri bermacam-macam mulai dari penyimpanan koleksi data tetap, digunakan dalam proses iterasi dalam perulangan(looping), fondasi dari matriks yang menggunakan array 2dimensi, dan masih banyak lagi. Dalam contoh aplikasi array biasanya digunakan dalam daftar dari suatu elemen misal dalam game daftar papan peringkat(leaderboard), dalam e-commerce daftar keranjang atau daftar barang.

------

## 2. Diketahui Stack berupa Linked List dengan kondisi mula-mula Stack kosong. Gambarkan Stack berupa Double Linked List tersebut beserta posisi penunjuknya (pointer), jika ada perintah :<br>a. Push(Top,60), Push(Top,40), Pop(Top,Item)<br>b. Push(Top,25), Pop(Top,Item), Pop(Top,Item)<br>c. Pop(Top,Item), Pop(Top,Item), Push(Top,50)
![image alt](https://github.com/fqhali/ETSStrukturData/blob/6f42f4dbc0a54212b493812c2d0857c6544cee5a/Screenshot%202026-04-28%20163613.png)
<br>
![image alt](https://github.com/fqhali/ETSStrukturData/blob/6f42f4dbc0a54212b493812c2d0857c6544cee5a/Screenshot%202026-04-28%20163657.png)
<br>
![image alt](https://github.com/fqhali/ETSStrukturData/blob/6f42f4dbc0a54212b493812c2d0857c6544cee5a/Screenshot%202026-04-28%20163710.png)

---------

## 3. Diketauhui Ekspresi berikut E = a + (2·b^3)/(f − g) + d·h<br>- Ubahlah ke dalam notasi Postfix<br>- Implementasikan menggunakan Stack dan buat screenshot eksekusinya.

notasi linear : a + (2 * b^3) / (f - g) + d * h <br>
notasi postfix : E a 2 b 3 ^ * f g - / + d h * + =
<br>
didapat dari:
```
b^3 =	b 3 ^
2 . b^3 = 2 b 3 ^ *
f - g = f g -
2 . b^3 / f - g = 2 b 3 ^ * f g - /
d * h = d h *
a + 2 . b^3 / f - g = a 2 b 3 ^ * f g - / +
a + 2 . b^3 / f - g + d * h = a 2 b 3 ^ * f g - / + d h * +
E = a + 2 . b^3 / f - g + d * h -> E a 2 b 3 ^ * f g - / + d h * + =
```
```cpp
#include <iostream>
#include <stack>
#include <string>
#include <cctype>

using namespace std;

int precedence(char op) {
    if (op == '^')
        return 3;
    if (op == '*' || op == '/')
        return 2;
    if (op == '+' || op == '-')
        return 1;
    return -1;
}

string infixToPostfix(string infix) {
    stack<char> st;
    string postfix = "";

    for (int i = 0; i < infix.length(); i++) {
        char c = infix[i];

        if (c == ' ') continue;

        if (isalnum(c)) {
            postfix += c;
        }
        else if (c == '(') {
            st.push('(');
        }
        else if (c == ')') {
            while (!st.empty() && st.top() != '(') {
                postfix += st.top();
                st.pop();
            }
            if (!st.empty()) {
                st.pop();
            }
        }
        else {
            while (!st.empty() && precedence(st.top()) >= precedence(c)) {
                if (c == '^' && st.top() == '^') {
                    break;
                }
                postfix += st.top();
                st.pop();
            }
            st.push(c);
        }
    }

    while (!st.empty()) {
        postfix += st.top();
        st.pop();
    }

    return postfix;
}

int main() {
    string infix = "a + (2 * b^3) / (f - g) + d * h";
    
    cout << "=== Program Konversi Infix ke Postfix ===" << endl;
    cout << "Ekspresi Infix  : " << infix << endl;
    
    string postfix = infixToPostfix(infix);
    
    cout << "Notasi Postfix  : " << postfix << endl;

    return 0;
}
```
![image alt](https://github.com/fqhali/ETSStrukturData/blob/3df2b5a1d4227432e83e691b20a1ed21306023ad/Screenshot%202026-04-28%20165608.png)

-----------------
## 4. Diketahui maksimum Queue = 9 elemen dengan kondisi mula-mula Queue kosong. Gambarkan Queue beserta posisi Front dan Rear, jika ada perintah :<br>a. Tambah Angka 19<br>b. Tambah Angka 7<br>c. Hapus 2 Angka<br>d. Tambah Angka 40<br>e. Hapus 3 Angka<br>f. Tambah Angka 18

![image alt](https://github.com/fqhali/ETSStrukturData/blob/18d101f531c7d7b772016718276318b5d3c537e4/queue.png)
