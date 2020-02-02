# Data-Works
Never settle

#include<windows.h>
#include<iostream>
#include<fstream>
#include<string>
using namespace std;
 typedef struct Air {
	string  Airnum;
	string planenum;
	string start;
	string des;
	string time;
	string level;
	int passenger_load;
	int remained;
	struct Air *next;
	struct passenger *next2;

}Air,*Linklist;
typedef struct passenger {
	string name;
	int booknumber;
	string level;
	struct passenger *next;
}passenger,*Link;
Linklist init();//初始化Air链表头结点
Link  init1();//初始化passenger链表头结点
Linklist input(Linklist q);//初始化航班信息
void dessearch(Linklist p);//按目的地查询航班信息
void  Airsearch(Linklist p);//按航班号查询航班信息
int search(Linklist p);//查询航班信息
int order(Linklist p, Link q);//订票函数
void cancel(passenger *head, string name);//退票函数
void add(Air *p, string Airnum, string planenum, string start, string des, string time, int passenger_load, int remained);//增加Air链表节点
void add1(passenger *p, string name, int booknumber, string level);//增加passenger链表节点
void print(Air *p);//打印航班信息
passenger* Delete(passenger *head, string name);//删除节点
void Menu();//菜单函数
passenger* Delete(passenger *head, string name) {
	passenger *p;
	passenger *pre=head;
	for (p = head->next; p != NULL; pre = pre->next, p = p->next)
	{
		if (p->name == name)
		{
			pre->next = p->next;
			break;
		}
	}
	if (!p)
		cout << "                   没有找到您的信息" << endl;
	return p;
}
Link init1() {
	passenger *head=new passenger();
	head->next = NULL;
	return head;
}
void add1(passenger *p, string name, int booknumber, string level)
{
	for (; p->next != NULL; p = p->next);
	passenger *q = new passenger();
	q->name = name;
	q->booknumber = booknumber;
	q->level = level;
	p->next = q;
	q->next = NULL;
}
Linklist init() {
	Air* head = new Air();
	Air *s;

	head->next = NULL;
	s = head;
	return s;
}
void add(Air *p, string Airnum, string planenum, string start, string des, string time,int passenger_load, int remained) {
	for (; p->next != NULL; p=  p->next);
	Air *q = new Air();
	q->Airnum = Airnum;
	q->planenum = planenum;
	q->start = start;
	q->des = des;
	q->time = time;
	q->remained = remained;
	q->passenger_load = passenger_load;
	p->next = q;
	q->next = NULL;
}

Linklist input(Linklist q) {
	//Linklist p=init();
	Air *p = new Air();
	q->next = p;
	string Airnum;
	string planenum;
	string start;
	string des;
	string time;
	int passenger_load;
	int remained;
	ofstream outfile("d:/test.txt", ios::app);
	outfile << "    ";
	outfile << "航班号";
	outfile << "   ";
	outfile << "飞机号";
	outfile << "   ";
	outfile << "飞行时间";
	outfile << "   ";
	outfile << "起始站";
	outfile << "   ";
	outfile << "终点站";
	outfile << "     ";
	outfile << "成员定额";
	outfile << "     ";
	outfile << "票余量";
	outfile <<endl;
	outfile << "    ";
	//outfile.close();
	if (p) {
		cout << "                   开始录入航班信息："<<endl ;
		cout << "                   输入航班号" << endl<<"                   ";
		cin >> Airnum;
		outfile << Airnum;
		outfile << "    ";
		p->Airnum = Airnum;
		cout << "                   输入飞机号：" <<endl<<"                   ";
		cin >> planenum;
		outfile << planenum;
		outfile << "    ";
		p->planenum = planenum;
		cout << "                   请输入起始站："<<endl<<"                   ";
		cin >>start;
		outfile << start;
		outfile << "    ";
		p->start = start;
		cout << "                   输入终点站：" <<endl<<"                   ";
		cin >> des;
		outfile << des;
		outfile << "    ";
		p->des = des;
		cout << "                   输入飞行日期："<<endl<<"                   " ;
		cin >> time;
		outfile << time;
		outfile << "    ";
		p->time = time;
		cout << "                   输入载客量：" <<endl<<"                   ";
		cin >>passenger_load;
		outfile << passenger_load;
		outfile << "    ";
		p->passenger_load = passenger_load;
		cout << "                   票余量："<<endl<<"                   " ;
		cin >> remained;
		outfile << remained;
		outfile << "    ";
		outfile << endl;
		outfile << endl;
		outfile.close();
		p->remained = remained;
	}
	p->next = NULL;
	return p;

}
void print(Air *p) {
	p = p->next;
	while (p != NULL)
	{
		passenger *q = p->next2;

		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_RED | FOREGROUND_BLUE);
		cout << "    " << "航班号  飞机号  飞行时间  起始站  终点站  乘员定额  票余量   " << endl;
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN);
		cout << "    " << p->Airnum << "    " << p->planenum << "    " << p->time << "    " <<p->start<<"    "<<p->des<<"      "<< p->passenger_load << "       " << p->remained << endl;
		if (q == NULL)
		{
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN);
			cout << "                   该航班暂无乘客" << endl;
		}
		int temp = 0;
		if (q!=NULL&&(q->name).length() == 0)
		{
			q = q->next;
		}
		while (q!= NULL) {
			if (temp == 0)
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN);
				cout << "                   以下为该航班乘客信息" << endl<<endl;
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN);
				cout << "                   姓名  购票数  舱位等级" << endl << endl;
			}
			temp++;
			
			cout << "                   "<<q->name << "   " << q->booknumber << "    " << q->level << endl<<endl;
			q = q->next;
		}
		p = p->next;
	}
}
void printone(Air *p) {
	passenger *q = p->next2;
	//q = q->next;
	if (p)
	{
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY|FOREGROUND_RED| FOREGROUND_BLUE);
		cout << "  " << "航班号  飞机号  飞行时间  起始站  终点站  乘员定额  票余量  " << endl;
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN);
		cout << "    " << p->Airnum << "    " << p->planenum << "    " << p->time << "    " << p->start << "    " << p->des << "      " << p->passenger_load << "       " << p->remained << endl;
		if (q == NULL)
		{
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY|FOREGROUND_BLUE| FOREGROUND_GREEN);
			cout << "                   该航班暂无乘客" << endl;
		}
		if (q != NULL && (q->name).length() == 0)
		{
			q = q->next;
		}
		int temp = 0;
		while (q != NULL) {
			if (temp == 0)
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_RED | FOREGROUND_BLUE);
				cout << "                   以下为该航班乘客信息" << endl << endl;
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN);
				cout << "                   姓名  购票数  舱位等级" << endl << endl;
			}
			temp++;
			cout << "                   " << q->name << "   " << q->booknumber << "    " << q->level << endl << endl;
			q = q->next;
		}
	}

	else
		return;
}
int search(Linklist p) {
	int n;
	//Linklist *p;
	system("cls");
	while (1) {
		//system("cls");
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_RED | FOREGROUND_BLUE);
		cout << "                   查找航线信息" << endl;
		cout << "                   通过航班号查询------1" << endl;
		cout << "                   通过目的地查询------2" << endl;
		cout << "                   返回主菜单----------3" << endl;
		cout << "                   退出系统------------4" << endl << endl;
		cout << "                   输入相应数字进行相应操作" << endl << "                   ";

		cin >> n;
		switch (n)
		{
		case 1:
			system("cls");
			Airsearch(p);
			break;
		case 2:
			system("cls");
			dessearch(p);
			break;
		case 3:
			system("cls");
			Menu();
			break;
		default:
			break;
		}
		if (n == 3||n==4)
			break;
	}
	return n;
}
void dessearch(Linklist p) {
	string s,judge;
//	int temp;
	Linklist temp1 = p;
	//Linklist p=init() ;
	cout << "                   请输入要查询的目的地：" ;
	cin >> s;
	do {
		p = p->next;
		if (p)
		{
		
			if (s==p->des)
			{
				printone(p);
			}
			
		}
		if (!p)
		break;
	} while (s != p->des||p != NULL);
	cout << "                   是否继续查询（输入“是”继续，输入“否”返回上一级）" << endl << "                   ";
	cin >> judge;
	if (judge == "是")
	{
		system("cls");
		dessearch(temp1);
	}
	else
	{
		system("cls");
		return;
	}
	if (!p) {
		cout << "                   对不起，您查询的目的地不存在" << endl;
		cout << "                   是否重新输入(输入“是”重新输入，输入“否”返回上一级菜单)" << endl << "                   ";
		cin >> judge;
		if (judge == "是")
		{
			system("cls");
			dessearch(temp1);
		}
		else
		{
			system("cls");
			return;
			//search(temp1);
		}
	}
}
void Airsearch(Linklist p) {
	string s, judge;
	Linklist temp1 = p;
	//int temp;
	//Linklist p=init();
cout << "                   请输入要查找的航班号：";
	cin >> s;
	do {
		p = p->next;
		if (p)
		{
			if (s == p->Airnum)
			{
				printone(p);
				cout << "                   是否继续查询（输入“是”继续，输入“否”返回上一级）" << endl << "                   ";
				cin >> judge;
				if (judge == "是")
				{
					system("cls");
					Airsearch(temp1);
				}
				else
				{
					system("cls");
					return;
				}
			}

		}
		if (!p)
			break;
	} while (s != p->Airnum);
	if (!p) {
		cout << "                   对不起，您输入的航班号不存在" << endl;
		cout << "                   是否重新输入(输入“是”重新输入，输入“否”返回上一级菜单)" << endl << "                   ";
		cin >> judge;
		if (judge == "是")
		{
			system("cls");
			Airsearch(temp1);
		}
		else
		{
			system("cls");
			return;
		}
	}
}
int order(Linklist p,Link q) {
	string s,name,level,s1;
	int checknum;
	Linklist temp = p;
	//Linklist p=init();
	cout << "                   请输入起始站：";
	cin >> s1;
	cout << "                   请输入终点站：";
	cin >> s;
	if (p) {
		do {
			p = p->next;
			if (!p)
			{
				int x;
				cout << "                   对不起，没有您要找的航班(如果继续订票则输入1，如果要取消订票请输入0)" << endl<<"                   ";
				cin >> x;
				if (x == 1)
				{
					order(temp,q);
					//return ;
				}
				if (x == 0)
				{
					system("cls");
					Menu() ;
					return x;
				}
			}
			if (s==p->des&&s1==p->start)
			{
				printone(p);

			}
		} while (s != p->des&&s1!=p->start);
		if (s == p->des&&s1==p->start)
		{

			do {
				cout << "                   请输入您的姓名：";
				cin >> name;
				cout << "                   请输入您要订的票数：";
				cin >> checknum;
				if (checknum > p->remained)
				{
					int i;
					cout << "                     票数不足" << endl << "                   ";
					cout << "                   是否重新订票(输入1重新订票，输入0退出订票)" << endl << "                   ";
					cin >> i;
					if (i == 1)
					{
						order(temp, q);
					}
					if (i == 0)
					{
						system("cls");
						Menu();
						return i;
					}
				}
				else
				{
					p->next2 = q;//p->next2==passenger的头结点；
					//Link q = init1();
					cout << "                   请输入舱位等级：";
					cin >> level;
					p->remained -= checknum;
					SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE  | FOREGROUND_RED);
					cout << endl;
					cout << "                     订票成功!" << endl;
					add1(q, name, checknum, level);
					q = q->next;

				}
			} while (s != p->des);
		}
	}
	
}
void cancel(passenger *head, string name) {
	passenger *p = Delete(head, name);
	if (p != NULL) {
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_RED);
		cout << endl;
		cout << "                     退票成功！" << endl;
	}
}

void Menu() {
	SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_RED| FOREGROUND_GREEN);
	cout << "                   *欢迎使用航空机票订票系统！*" << endl;
	cout << "                   *读取航班信息----------0   *" << endl;
	cout << "                   *初始化航班信息--------1   *" << endl;
	cout << "                   *查看航班信息----------2   *"<< endl;
	cout << "                   *订票------------------3   *" << endl;
	cout << "                   *查询------------------4   *" << endl;
	cout << "                   *退票------------------5   *" << endl;
	cout << "                   *退出系统--------------6   *" << endl;
	cout << "                   *清屏------------------7   *" << endl;
}
int main() {
	//system("color F0");
	Air *temp0=NULL;
	int count = 0;
	Menu();
	int n;
	Linklist head=init();
	Link head1 = init1();

	//Menu();
L:cout << "                   请输入数字:";
	cin >> n;
	if (n == 0)
	{  
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN );
		string filename = "d:/test.txt";
		ifstream infile(filename.c_str());
		string temp;
		if (!infile.is_open()) {
			cout << "打开文件失败" << endl;
		}
		while (getline(infile, temp)) {
			cout << temp << endl;
		}
	//	Air *q = input(head);
		if (count == 0) {
			Air *q = head;
			add(q, "CA1544", "A733", "合肥", "北京", "1.3.5", 200, 200);
			Air *m = q->next;
			add(m, "MU5341", "M90", "上海", "广州", "2.4.6", 150, 150);
			Air *d = m->next;
			add(d, "CZ3869", "733", "重庆", "深圳", "2.3.4", 300, 300);
			Air *u = d->next;
			add(u, "CZ3860", "520", "长沙", "郑州", "1.1.1", 200, 200);
			temp0 = u->next;
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
			cout << "                   请输入相应数字继续操作" << endl;
			count++;
		}
		goto L;
	}

	
		switch (n)
		{
		case 1:

		{   ofstream outfile("d:/test.txt", ios::app);
			system("cls");
			string judge,ifcontinue;
			Air *q1;
			//head = init();
			if (temp0)
				q1 = input(temp0);
			else
				q1 = input(head);
		B:	
			cout << "                   是否继续录入航班信息(输入“是”继续，输入其他停止录入)" << endl<<"                   ";
			cin >> ifcontinue;
			if (ifcontinue == "是") {
				outfile << "    ";
				outfile << "航班号";
				outfile << "   ";
				outfile << "飞机号";
				outfile << "  ";
				outfile << "飞行时间";
				outfile << "   ";
				outfile << "起始站";
				outfile << "   ";
				outfile << "终点站";
				outfile << "   ";
				outfile << "成员定额";
				outfile << "   ";
				outfile << "票余量";
				outfile << endl;
				outfile << "    ";
				//outfile.close();
				system("cls");
				string s1, s2, s3, s4,s5;
				int a1, a2;
				cout << "                   输入航班号:" << endl<<"                   ";
				cin >> s1;
				outfile << s1; 
				outfile << "     ";
				cout << "                   输入飞机号:" << endl<<"                   ";
				cin >> s2;
				outfile << s2;
				outfile << "     ";
				cout << "                   输入起始地:" << endl<<"                   ";
				cin >> s3;
				outfile << s3;
				outfile << "     ";
				cout << "                   输入目的地:" << endl<<"                   ";
				cin >> s4;
				outfile <<s4;
				outfile << "       ";
				cout << "                   输入起飞时间:" << endl<<"                   ";
				cin >> s5;
				outfile <<s5;
				outfile << "    ";
				cout << "                   输入载客量:" << endl << "                   ";
				cin >> a1;
				outfile << a1;
				outfile << "       ";
				cout << "                   输入票余量:" << endl<<"                   ";
				cin >> a2;
				outfile <<a2; 
				outfile << "     ";
				outfile << endl;
				outfile << endl;
				//outfile.close();
				add(q1, s1, s2, s3, s4, s5, a1, a2);
				q1 = q1->next;
				goto B;
			}
			outfile.close();
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_RED | FOREGROUND_BLUE);
			cout << endl;
			cout << "                   航班信息初始化成功!" << endl << endl;
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN|FOREGROUND_RED);
			cout << "                   是否继续操作(输入“是”返回主菜单继续操作，输入其他退出系统)" << endl;
			cin >> judge;
			if (judge == "是")
			{   
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
			//	cout << "                   请输入相应数字进行操作" << endl<<"                   ";
				//cin >> n;
				system("cls");
				Menu();
				goto L;

			}
			else
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				cout << "                   系统已退出，欢迎下次使用";
				system("pause");
			}
		}
		break;
		case 2:
		{    string judge;
	    //int temp;
		system("cls");
			print(head);
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
			cout << "                   是否继续操作(输入“是”返回主菜单继续操作，输入其他退出系统)" << endl<<"                   ";
			cin >> judge;
			if (judge == "是")
			{   
				system("cls");
				Menu();
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				//cout << "               请输入相应数字进行操作" << endl<<"                   ";
				//cin >> n;
				goto L;

			}
			else
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				cout << "                   系统已退出，欢迎下次使用";
				system("pause");
			}
		}
			break;
		case 3:
		{    string judge;
		     system("cls");
		int temp3 = order(head, head1);
		if (temp3 == 0)
		{
			goto L;
		  }
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
			cout <<"                    是否继续操作(输入“是”返回主菜单继续操作，输入其他退出系统)" << endl<<"                   ";
			cin >> judge;
			if (judge == "是")
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				//cout << "                  请输入相应数字进行操作" << endl<<"                   ";
				//cin >> n;
				system("cls");
				Menu();
				goto L;

			}
			else
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				cout << "                   系统已退出，欢迎下次使用";
				system("pause");
			}
		}
			break;
		case 4:
		{   int temp;
			string judge;
			temp=search(head);
			if (temp == 3)
			{  
				goto L;
			}
			if (temp == 4)
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				cout << "                   系统已退出，欢迎下次使用";
				system("pause");
			}


		}
			break;
		case 5:
		{    system("cls");
			string name,judge;
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
			cout << "              请输入您的姓名" << endl<<"                   ";
			cin >> name;
			cancel(head1, name);
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
			cout <<"                   是否继续操作(输入“是”继续返回主菜单操作，输入其他退出系统)" << endl<<"                   ";
			cin >> judge;
			if (judge == "是")
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				system("cls");
				Menu();
				//cout << "                   请输入相应数字进行操作" << endl<<"                   ";
				//cin >> n;
				goto L;

			}
			else
			{
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
				cout << "                   系统已退出，欢迎下次使用";
				system("pause");
			}
		}
		break;
		case 6:
			SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_RED);
			cout << "                   系统已退出，欢迎下次使用";
			system("pause");
			break;
		case 7:
			system("cls");
			Menu();
			goto L;
			break;
		default:
			break;
		}
	}


