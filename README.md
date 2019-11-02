
#include <iostream>
#include <algorithm>
#include <fstream>
#include <string>
#include <vector>
#include <stdio.h>
#include <experimental/filesystem>
#include <windows.h>

using namespace std;
namespace fs = std::experimental::filesystem;
void checkInt(int &Value);


class CBOOK{

	static unsigned int index;
	string title;
	string author;

public:

	static int w_books(CBOOK  &obj) {
		cout << "Menu" << endl;
		cout << "1.Add new book" << endl;
		cout << "2.Show list witn book" << endl;
		cout << "3.Search book" << endl;
		cout << "4.Return in main menu" << endl;

		int choise;
		cin >> choise;
		checkInt(choise);

		string pathB = "books.txt";

		ofstream foutB;
		ifstream finB;
		

		 
		//	while(true) {
		switch (choise)
		{
		case 1:
			

			foutB.open(pathB, ifstream::app);
			if (!foutB.is_open()) { cout << "File is not opened!" << endl; }
			else
			{
				index++;
				//cout << "File is opened :)" << endl;
				//cout << "Write the index of the book" << endl;
				//cin >> obj.index[SIZE];
				foutB << obj.index<<" ";
				cout << "Write the title of the book" << endl;
				cin >> obj.title;
				foutB << obj.title<<" ";
				cout << "Write the author of the book" << endl;
				cin >> obj.author;
				foutB << obj.author<<" ";

				foutB<<"\n"<<endl;
				foutB.close();

			}
			break;
			//return 0;
		case 2:
			finB.open(pathB);
			
			if (!finB.is_open()) { cout << "File is not opened!" << endl; }
			
			else
			{
				string str;
			//	cout << "File is opened :)" << endl;
				
				cout << "The list if books: " << endl;
				while (getline(finB,str)) {
					
					cout<<str<<"\n";

				}

				

			}
			finB.close();
			//return 0;
			break;
		case 3:
			finB.open(pathB);

			if (!finB.is_open()) { cout << "File is not opened!" << endl; }
			else
			{
				//cout << "File is opened :)" << endl;
				string search;
				cout << "Input something for searching:" << endl;
				cin >> search;
				vector <string> v;
				string str;
				bool flag = false;
				const int N = 50;
				while (getline(finB, str)) {
					size_t i = 0;
					while (true)
					{
						i = str.find(search, i);
						if (i != string::npos)
						{
							i += search.size();
							string temp;
							temp.append(str);
							v.push_back(temp);
							i += N;
						}
						else if (i = string::npos) {
							if (!flag)
							{
								cout << "Nothing is found" << endl;
								flag = true;
							}
							break;
						}
					}
				}
				

				for (size_t i = 0; i < v.size(); ++i) { 
					cout << "The result of searching:" << endl;
					cout << v[i] << endl; }
				

			}
			finB.close();
			break;
			//return 0;
		case 4:

			system("cls");
			return 0;
		default:
			system("cls");
			cout << "Try again!" << endl;
			//return 0;

		}
	}
	static string  deleteBook(string bookIndex)
	{
		string pathB = "books.txt";
		string tempPath = "temp.txt";

		ofstream foutT;
		ifstream finB;
		finB.open(pathB);
		foutT.open(tempPath);
		if (!finB.is_open()) { cout << "File is not opened!" << endl; }
		else
		{
			//cout << "File is opened :)" << endl;
		
		
			string deletedString;
			string str;
			bool flag = false;
			const int N = 50;
			while (getline(finB, str)) {
				size_t i = 0;
				
					i = str.find(bookIndex, i);
					if (i != string::npos)
					{
						i += bookIndex.size();
						deletedString.append(str);
						
						i += N;
					}
					else {
						//i += bookIndex.size();
						string temp;
						temp.append(str);
						foutT << temp << "\n";
						i += N;
					}
			}
			foutT.close();
			finB.close();
			
			fs::remove("books.txt");
			fs::rename("temp.txt","books.txt");

			
			return deletedString;
		}
	}
};
unsigned int CBOOK::index = 0;


class CREADER {
	string  takenBook;
	string name;
	string surname;
	
public:
	
	
	int w_readers(/*CREADER &obj*/) {
		cout << "Menu" << endl;
		cout << "1.Add new reader" << endl;
		cout << "2.Show list with readers" << endl;
		cout << "3.Search reader" << endl;
		cout << "4.Take a book" << endl;
		cout << "5.Bring the book back" << endl;
		cout << "6.Return in main menu" << endl;


		ofstream foutR;
		ifstream finR;
		string pathR = "readers.txt";

		int choise;
		cin >> choise;
		checkInt(choise);
		string strR = this->getName() + this->getSurname();
		string bookIndex; // for case 4 
		// for case 5
		string pathB = "books.txt";
		ofstream foutB;
		foutB.open(pathB, ifstream::app);
		//string strR = name + surname;
		switch (choise)
		{
		case 1:
			foutR.open(pathR, ifstream::app);
			if (!foutR.is_open()) { cout << "File is not opened!" << endl; }
			else
			{
				//cout << "File is opened :)" << endl;
				cout << "Write the name" << endl;
				cin >> this->name;
				foutR << name << " ";
				cout << "Write the surname" << endl;
				cin >> surname;
				foutR << surname << " ";


				foutR << "\n" << endl;

				foutR.close();

			}


			break;
		case 2:

			finR.open(pathR);

			if (!finR.is_open()) { cout << "File is not opened!" << endl; }
			else
			{
				//cout << "File is opened :)" << endl;
				cout << "The list of readers: " << endl;
				while (getline(finR, strR)) {

					cout << strR << "\n";

				}

				finR.close();

			}


			break;
		case 3:

			finR.open(pathR);

			if (!finR.is_open()) { cout << "File is not opened!" << endl; }
			else
			{
				//cout << "File is opened :)" << endl;
				string search;
				cout << "Input something for searching:" << endl;
				cin >> search;
				vector <string> v;
				string str;
				const int N = 50;
				bool flag = false;
				while (getline(finR, str)) {
					size_t i = 0;
					while (true)
					{
						i = str.find(search, i);
						if (i != string::npos)
						{
							i += search.size();
							string temp;
							temp.append(str);
							v.push_back(temp);
							i += N;
						}
						else /*if (i = string::npos)*/
						{
							if (!flag)
							{
								cout << "Nothing is found" << endl;
								flag = true;
							}
							break;
						}
					}
				}
				cout << "The result of searching:" << endl;
				for (size_t i = 0; i < v.size(); ++i) { cout << v[i] << endl; }
				finR.close();

			}
			break;

		case 4:
			cout << "Enter index of the book you want to take :" << endl;
			
			cin >> bookIndex;
			setTakenBook(CBOOK::deleteBook(bookIndex));

			break;
		case 5:

			foutB << getTakenBook();
			foutB.close();
			break;
		case 6:
			system("cls");
			return 0;

		default:
			system("cls");
			cout << "Try again!" << endl;
			break;

		}
	}
		string getName()
		{
			return this->name;

		}
		string getSurname()
		{
			return this->surname;

		}
		void setTakenBook(string takenBook) {
			this->takenBook = takenBook;
		}
		string getTakenBook()
		{
			return this->takenBook;

		}

};


	int main()
	{

		//ofstream foutR;
		//ifstream finR;
		CBOOK objB;
		CREADER objR;
		while (true) {
			cout << "Chooise something" << endl;
			cout << "Menu" << endl;
			cout << "1.Work with readers" << endl;
			cout << "2.Work with books" << endl;
			cout << "3.Exit" << endl;
			int choise;
			cin >> choise;
			checkInt(choise);
			switch (choise)
			{
			case 1: objR.w_readers();
				break;
			case 2: CBOOK::w_books(objB);
				break;
			case 3: return 0;
				break;
			default:
				cout << "Try again!" << endl;
			}

		}

		int a;
		cin >> a;

	}

	void checkInt(int &Value) {
		while (cin.fail() || cin.get() != '\n' || Value < 0) {

			cout << "Enter correct" << endl;

			cin.clear();

			rewind(stdin);

			cin >> Value;
		}
	}









