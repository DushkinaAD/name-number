#include <iostream>
#include <stdio.h>
#include <string>
#include <cstring>
#include <cmath>
#include <fstream>
#include <math.h>
using namespace std;

struct person{
	basic_string <char> name;
	basic_string <char> phone;
}tab[100];

int maxnumber(int n) {
	int max = 0;
	if (n == 1)
		max = tab[0].phone.length();
	else {
		for (int i = 0; i < n; i++) {
			if (tab[i].phone.length() > max)
				max = tab[i].phone.length();
		}
	}
	if (max >= 6)
		return max;
	else
		return 6;
}

int maxlen(int n) {
	int max = 0;
	if (n == 1)
		max = tab[0].name.length();
	else {
		for (int i = 0; i < n; i++) {
			if (tab[i].name.length() > max)
				max = tab[i].name.length();
		}
	}
	if (max >= 8)
		return max;
	else
		return 8;
}

void probel(int a, int max) {
	for (int i = 0; i < (max - a + 1); i++)
		cout << " ";
}

void probelnumber(int a, int num) {
	for (int i = 0; i < (num - a + 1); i++)
		cout << " ";
}

void dash(int max, int num) {
	for (int i = 0; i < (4 + max + num + 6); i++) {
		cout << "-";
	}
	cout << endl;
}

void print_all(int n) {
	int max = maxlen(n);
	int num = maxnumber(n);
	dash(max, num);
	cout << "|№ |" << " Фамилия";
	probel(8, max);
	cout << " |";
	cout << " Номер";
	probelnumber(6, num);
	cout << " |" << endl;
	dash(max, num);

	for (int i = 0; i < n; i++) {
		cout << "|" << i + 1 << " | ";
		cout << tab[i].name;
		probel(tab[i].name.length(), max);
		cout << "| ";
		cout << tab[i].phone;
		probelnumber(tab[i].phone.length(), num);
		cout << "|" << endl;
		dash(max, num);
	}
	cout << endl;
}

void vvod(int k, int n) {
	for (int i = k; i < n; i++) {
		cin.ignore();
		int s = 0;
		cout << "Фамилия " << (i + 1) << endl;
		int a = 0;
		string alf = "aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ";
		while (((a < 1) or (a > 25)) or ((s == 0) or (s != a))) {
			s = 0;
			getline(cin, tab[i].name);
			a = tab[i].name.length();
			if ((a < 1) or (a > 25))
				cout << "Повторите ввод (фамилия должна быть > 1 символа и < 25)" << endl;
			for (int p = 0; p < a; p++) {
				for (int j = 0; j < 52; j++) {
					if (tab[i].name[p] == alf[j])
						s++;
				}
			}
			if (s != a)
				cout << "Фамилия должна состоять только букв английского алфавита" << endl;
		}
		s = 0;
		string num = "0123456789";
		cout << "Номер телефона" << endl;

		while ((a < 3) or (a > 11) or (s == 0) or (s != a)) {
			s = 0;
			getline(cin, tab[i].phone);
			a = tab[i].phone.length();
			if ((a < 3) or (a > 11))
				cout << "Повторите ввод (номер телефона должен быть > 3 символов и < 11)" << endl;
			for (int p = 0; p < a; p++) {
				for (int j = 0; j < 10; j++) {
					if (tab[i].phone[p] == num[j])
						s++;
				}
			}
			if (s != a)
				cout << "Номер телефона должен состоять только из арабских цифр" << endl;
		}
		cout << "Для продолжения нажмите Enter" << endl;
	}
}

inline void vvod() {
	//FILE* fp;
	
	string line;
	ifstream in("test_1.txt"); 
	string alf = "aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ";
	string num = "0123456789";
	int p = 0;
	int q = 0;
	if (in.is_open()){
		while (getline(in, line)){
			if ((q != 0) or (q != 1))
				p = (q / 2);
			int n = line.length();
			int a = 0;
			int b = 0;
			for (int j = 0; j < n; j++) {
				for (int i = 0; i < 52; i++) {
					if (line[j] == alf[i])
						a++;
				}
			}
			for (int j = 0; j < n; j++) {
				for (int i = 0; i < 10; i++) {
					if (line[j] == num[i])
						b++;
				}
			}
			if (n == a)
				tab[p].name = line;
			if (n == b)
				tab[p].phone = line;
			q++;
		}
	}
	in.close();
	print_all(p +1);
}

inline void print_f(int n) {
	ofstream out;          
	out.open("test_2.txt");      
	if (out.is_open()){
		for (int i = 0; i < n; i++) {
			out << tab[i].name << endl;
			out << tab[i].phone << endl;
		}
	}
	out.close();
	cout << "Данные успешно записаны в файл" << endl;
}

void sizesort(int n) {
	for (int j = 1; j < n; j++) {
		for (int i = 0; i < n - j; i++) {
			int a = tab[i].name.length();
			int b = tab[i + 1].name.length();
			if (a > b) {
				string a1 = tab[i].name;
				tab[i].name = tab[i + 1].name;
				tab[i + 1].name = a1;
				string a2 = tab[i].phone;
				tab[i].phone = tab[i + 1].phone;
				tab[i + 1].phone = a2;
			}
		}
	}
}

int alf(int i) {
	string alf = "aA bB cC dD eE fF gG hH iI jJ kK lL mM nN oO pP qQ rR sS tT uU vV wW xX yY zZ";
	int a1 = tab[i].name.length();
	int a2 = tab[i + 1].name.length();
	int a;
	if (a1 > a2)
		a = a2;
	else
		a = a1;
	int q1 = 0;
	int q2 = 0;
	for (int j = 0; j < a; j++) {
		if (tab[i].name[j] != tab[i + 1].name[j]) {
			for (int p = 0; p < 77; p++) {
				if (tab[i].name[j] == alf[p])
					q1 = p;
				if (tab[i + 1].name[j] == alf[p])
					q2 = p;
			}
			if (abs(q2 - q1) > 1) {
				if (q1 < q2)
					return 1;
				else
					return 0;
			}
		}
	}
}

void alfsort(int n) {
	for (int j = 1; j < n; j++) {
		for (int i = 0; i < (n - j); i++) {
			if (alf(i) == 0) {
				string a1 = tab[i].name;
				tab[i].name = tab[i + 1].name;
				tab[i + 1].name = a1;
				string a2 = tab[i].phone;
				tab[i].phone = tab[i + 1].phone;
				tab[i + 1].phone = a2;
			}
		}
	}
}


int main() {

	while (true) {
		setlocale(LC_ALL, "Russian");
		int n = 0;
		int v = 0;
		cout << "Ручной ввод данных (1), ввод из TXT файла (2)" << endl;
		while ((v != 1) and (v != 2)) {
			cin >> v;
			if ((v != 1) and (v != 2))
				cout << "Выберете один из предложенный вариантов" << endl;
		}
		int var = 0;
		switch (v) {

		case 1:
			
			while (var != 7) {
				var = 0;
				cout << "Меню:" << endl;
				cout << "1 - Добавить данные" << endl;
				cout << "2 - Отсортировать по алфавиту" << endl;
				cout << "3 - Отсортировать по длине фамилии" << endl;
				cout << "4 - Вывести таблицу" << endl;
				cout << "5 - Записать в TXT файл" << endl;
				cout << "6 - Завершить работу" << endl;
				while ((var < 1) or (var > 7)) {
					cin >> var;
					if ((var < 1) or (var > 7))
						cout << "Выберете один из предложенный вариантов" << endl;
				}

				switch (var) {

				case 1:
					if (n == 0) {
						cout << "введите количество записей, которые хотите добавить (максимум 100)" << endl;
						while ((n < 1) or (n > 100)) {
							cin >> n;
							if ((n < 1) or (n > 100))
								cout << "Повторите ввод" << endl;
						}
						vvod(0, n);
						cout << endl;
						system("cls");
						cout << "Пользователь ввел следующие данные: " << endl;
						print_all(n);
					}
					else {
						int k = 0;
						cout << "Введите количество записей, которые хотите добавить (максимум 100)" << endl;
						while ((k < 1) or (k > 100)) {
							cin >> k;
							if ((k < 1) or (k > 100))
								cout << "Повторите ввод" << endl;
						}
						int a = k;
						k = n;
						n = k + a;
						vvod(k, n);
						cout << endl;
						system("cls");
						cout << "Пользователь ввел следующие данные: " << endl;
						print_all(n);
					}
					break;

				case 2:
					if (n == 0) {
						system("cls");
						cout << "Прежде чем сортировать, необходимо добавить данные" << endl;
						cout << endl;
					}
					else {
						cout << "Данные в алфавитном порядке: " << endl;
						alfsort(n);
						print_all(n);
					}
					break;

				case 3:
					if (n == 0) {
						system("cls");
						cout << "Прежде чем сортировать, необходимо добавить данные" << endl;
						cout << endl;
					}
					else {
						cout << "Данные по длине: " << endl;
						sizesort(n);
						print_all(n);
					}
					break;

				case 4:
					print_all(n);
					break;

				case 5:
					print_f(n);
					break;

				case 6:
					cout << "Благодарим за использование нашего сервиса" << endl;
					break;
				}
			}
			break;

		case 2:
			vvod();

			while (var != 5) {
				var = 0;
				cout << "Меню:" << endl;
				cout << "1 - Отсортировать по алфавиту" << endl;
				cout << "2 - Отсортировать по длине фамилии" << endl;
				cout << "3 - Вывести таблицу" << endl;
				cout << "4 - Завершить работу" << endl;
				while ((var < 1) or (var > 4)) {
					cin >> var;
					if ((var < 1) or (var > 4))
						cout << "Выберете один из предложенный вариантов" << endl;
				}

				switch (var) {

				case 1:
					cout << "Данные в алфавитном порядке: " << endl;
					alfsort(n);
					print_all(n);
					break;

				case 2:
					cout << "Данные по длине: " << endl;
					sizesort(n);
					print_all(n);
					break;

				case 3:
					print_all(n);
					break;

				case 4:
					cout << "Благодарим за использование нашего сервиса" << endl;
					break;
				}
			}
			break;
		}
		system("pause");
		system("cls");
	}
}
