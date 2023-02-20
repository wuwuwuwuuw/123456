#define _CRT_SECURE_NO_WARNINGS 1
#include<cstdio>
#include<iostream>
#include<string>	
#include<cmath>
#include<algorithm>
#include<map>
#include<cstring>
#include<Windows.h>
#include<stdlib.h>
using namespace std;

typedef struct student {
	char id[10];
	char name[20];
	char surname[20];
	char age[5];
	char classs[5];
	char note[100];
}stu;
typedef struct Llist {
	stu data;
	struct Llist* next;
	struct Llist* prior;

}Lnode, * List;
List L=NULL;//链表
void Add_Printf();
void printf_geren(Lnode* s);
Lnode* serch_id(List L, char id[]);
void initList(List* L);
void copy_string(char from[], char to[]);
Lnode* createLnode(stu h);
void initList(List* L);
int Listempty(List L);
void munu();
void systeminto();
void save(List* L);
void read(List* L);
stu* deletenode(List* L, stu* data, char id[]);

void initList(List* L)//初始化 创造一个头结点这个已测试无错
{

	(*L) = (Lnode*)malloc(sizeof(Lnode));				//创造一个头结点//双向链表要改
	(*L)->next = NULL;
	(*L)->prior = NULL;

}

void copy_string(char from[], char to[])
{
	int i = 0;
	while (from[i] != '\0')
	{
		to[i] = from[i];
		i++;
	}
	to[i] = '\0';
}

Lnode* createLnode(stu h)//双向链表要改
{
	Lnode* P;
	P = new Lnode;
	P->data = h;
	P->prior = NULL;
	P->next = NULL;
	return P;
}
//判断单链表是否为空 空为1，非空0，这个已测试无错
int Listempty(List L)//在这个函数中我只需要链表的地址里面的内容，并不需要改变内
{
	if (L->next)return 0;
	else return 1;
}

Lnode* serch_id(List L, char id[])//查询ID
{
	Lnode* p = L->next;
	if (p == NULL) { printf("查无此人\n"); }
	else
	{
		while (p)
		{
			if (strcmp(p->data.id, id)==0)
			{
				return p;

			}
			p = p->next;
		}
	}
	return p;
}

void fixnode(List* L, char id[])//修改
{
	system("cls");
	Lnode* p = serch_id((*L), id);
	if (p == NULL)return;
	while (1)
	{
		printf("已查到该生的相关信息：");
		printf_geren(p);
		printf("请选择所要修改的学生信息类：\n");
		printf("修改姓名 ---- 1\n");
		printf("修改性别 ---- 2\n");
		printf("修改班级 ---- 3\n");
		printf("修改年龄 ---- 4\n");
		printf("修改备注 ---- 5\n");
		printf("修改 ID ----- 6\n");
		printf("请输入需要修改的信息：");
		int choice;
		scanf("%d", &choice);
		switch (choice)
		{
		case 1:
			printf("请输入姓名：");
			scanf("%s", p->data.name);
			printf("\n");
			break;
		case 2:
			printf("请输入性别：");
			scanf("%s", p->data.surname);
			printf("\n");
			break;
		case 3:
			printf("请输入班级：");
			scanf("%s", p->data.classs);
			printf("\n");
			break;
		case 4:
			printf("请输入年龄：");
			scanf("%s", p->data.age);
			printf("\n");
			break;
		case 5:printf("请输入备注：");
			scanf("%s", p->data.note);
			printf("\n");
			break;
		case 6:
			printf("请输入ID：");
			scanf("%s", p->data.id);
			printf("\n");
			break;
		default:
			printf("输入错误，请重新输入");
			system("cls");
			break;
		}
	printf("是否继续修改该学生信息？（是：1 / 否：0）;\n");

	int show = 0;
	scanf("%d", &show);
	printf("\n");
	if (show == 1)continue;
	else return;
	}
	


}
void findstuent(List L)//查询
{
	system("cls");
	int choice = 0;
	printf("请选择查询方式:");
	printf("按照学号查询 ---- 1\n");
	printf("按照姓名查询 ---- 2\n");
	printf("按照性别查询 ---- 3\n");
	printf("按照年龄查询 ---- 4\n");
	printf("请输入查询方式：");
	scanf_s("%d", &choice);
	char id[5];
	char name[50];
	char sex[50];
	char age[5];
	Lnode* p = L->next;
	if (choice == 1)
	{

		printf("请输入要查询的学号：");
		scanf("%s", id);
		if (p == NULL) { printf("查无此人\n"); }
		else
		{
			while (p)
			{
				if (strcmp(p->data.id, id)==0)
				{
					printf_geren(p);//显示个人信息
					break;
				}
				p = p->next;
			}
		}
	}
	else if (choice == 2)
	{
		printf("请输入要查询的姓名：");
		scanf("%s", name);
		if (p == NULL) { printf("查无此人\n"); }
		else
		{
			while (p)
			{
				if (strcmp(name, p->data.name) == 0)
				{
					printf_geren(p);//显示个人信息

				}
				p = p->next;
			}
		}
	}
	else if (choice == 3)
	{
		printf("请输入要查询的性别：");
		scanf("%s", sex);
		if (p == NULL) { printf("查无此人\n"); }
		else
		{
			while (p)
			{
				if (strcmp(sex, p->data.surname) == 0)
				{
					printf_geren(p);//显示个人信息

				}
				p = p->next;
			}
		}

	}
	else if (choice == 4)
	{
		printf("请输入要查询的年龄：");
		scanf("%s", age);
		if (p == NULL) { printf("查无此人\n"); }
		else
		{
			while (p)
			{
				if (strcmp(p->data.age, age)==0)
				{
					printf_geren(p);//显示个人信息

				}
				p = p->next;
			}
		}
	}
}

void printf_geren(Lnode* s)
{

	printf("________________________________________________________________\n");
	printf("|学号\t|姓名\t|性别\t|班级\t|年龄\t|备注\t|\n");
	printf("|%s\t|%s\t|%s\t|%s\t|%s\t|%s\t\n", s->data.id, s->data.name, s->data.surname, s->data.classs, s->data.age, s->data.note);
	printf("________________________________________________________________\n");
}

void insertLlist(List* L, Lnode k)//双向链表
{
	Lnode* p = (*L);
	Lnode* s = createLnode(k.data);
	if (p->next != NULL)
	{
		p->next->prior = s;
		s->next = p->next;
		p->next = s;
		s->prior = p;
	} 
	else {
		p->next = s;
		s->prior = p;
	}
}
void Add_Printf()//
{
	system("cls");
	Lnode st;
	printf("请输入新增学生的相关信息：\n");
	printf("学号：");
	scanf("%s", st.data.id);
	printf("姓名：");
	scanf("%s", st.data.name);
	printf("性别：");
	scanf("%s", st.data.surname);
	printf("班级：");
	scanf("%s", st.data.classs);
	printf("备注：");
	scanf("%s", st.data.note);
	printf("年龄:");
	scanf("%s", st.data.age);
	insertLlist(&L, st);
}

stu* deletenode(List* L, stu* data, char id[])
{
	Lnode* p = (*L);
	if (!Listempty) {
		printf("数据库中没有任何信息\n");
	}
	else {
		Lnode* t = serch_id(p, id);
		if (t == NULL)printf("此人信息已经被删除\n");
		else if(t->next!=NULL)
		{
			*data = t->data;
			t->prior->next = t->next;
			t->next->prior = t->prior;
			delete t;
		}
		else if (t->next == NULL)
		{
			*data = t->data;
			t->prior->next = t->next;;
		}
	}
	return data;
}

void printdLlist(Lnode* L)
{
	L = L->next;

	while (L)
	{

		printf_geren(L);
		L = L->next;

	}
	cout << endl;

}


void save(List* L)
{
	Lnode* p = (*L);
	FILE* file = fopen("学生信息.txt", "w");
	if (file == NULL) {
		printf("储存学生信息失败\n");
		return;
	}
	while (p->next != NULL)
	{
		p = p->next;
		fprintf(file, "%s\t%s\t%s\t%s\t%s\t%s\n", p->data.id, p->data.name, p->data.surname, p->data.age, p->data.classs, p->data.note);

	}
	printf("已保存当前已有学生信息\n");
	fclose(file);
}
void read(List* L)
{
	Lnode* p = (*L);
	FILE* rfile = fopen("学生信息.txt", "r");
	if (rfile == NULL)
	{
		printf("没有信息可以去读取\n");
		return;
	}
	Lnode k;
	while (fscanf(rfile, "%s\t%s\t%s\t%s\t%s\t%s\n", k.data.id, k.data.name, k.data.surname, k.data.age, k.data.classs, k.data.note) != EOF)
	{
		insertLlist(&p, k);
	}
	fclose(rfile);
}
void munu()
{
	
	int choics = 0;
	printf("欢迎您使用学生信息管理系统\n");
	int show = 0;
	printf("请选择是否显示菜单1/0\n");
	scanf_s("%d", &show);
	system("cls");

hhhe:	if (show == 1)
{
	printf(" \n\n                    \n\n");
	printf("  ******************************************************\n\n"); Sleep(10);
	printf("  *                学生信息管理系统                    *\n \n"); Sleep(10);
	printf("  --------------------------------------------------------\n\n"); Sleep(10);
	printf("*********************系统功能菜单*************************       \n"); Sleep(10);
	printf("     ----------------------   ----------------------   \n"); Sleep(10);
	printf("     *********************************************     \n"); Sleep(10);
	printf("     * 0.系统简介	 * *  1.录入学生信息   *     \n"); Sleep(10);
	printf("     *********************************************     \n"); Sleep(10);
	printf("     * 2.查询学生信息    * *  3.修改学生信息   *     \n"); Sleep(10);
	printf("     *********************************************     \n"); Sleep(10);
	printf("     * 4.删除学生信息    * *  5.显示学生信息   *     \n"); Sleep(10);
	printf("     *********************************************     \n"); Sleep(10);
	printf("     * 6.保存学生信息    * *  7.退出信息系统	*     \n"); Sleep(10);
	printf("     ********************** **********************     \n"); Sleep(10);
	printf("请选择功能\t\n"); Sleep(100);
	printf("编号选择：\t[0]\t[1]\t[2]\t[3]\t[4]\t[5]\t[6]\t[7]\n"); Sleep(100);
	scanf_s("%d", &choics);
	printf("您的选择是\t%d", choics);
	system("cls");
	
	stu data = { "0","0","0","0","0","0" };
	int num = 0;
	char id[5];
	char isAccount[20] = { "1" };
	char isPassword[20] = { "w" };
	char Account[20];
	char Password[20];

	switch (choics)
	{
	case 0:
		systeminto();

		break;
	case 1:
		printf("请输入要录入学生信息的人数\n");

		scanf_s("%d", &num);
		while (num--)Add_Printf();
		break;

	case 2:
		findstuent(L);
		break;
	case 3:
	pw:printf("请输入账号和密码\n");
		printf("账号:\n");
		scanf("%s", Account);
		printf("密码:\n");
		scanf("%s", Password);
		if (strcmp(Account,isAccount)==0 && strcmp(Password ,isPassword)==0)
		{
			printf("请输入修改同学信息的id\n");
			scanf("%s", id);
			fixnode(&L, id);
		}
		else {
			printf("账号或密码错误，请重新输入\n");
			goto pw;
		}
		break;
	case 4:
		printf("请输入要删除同学信息的id\n");
		scanf("%s", id);
		deletenode(&L, &data, id);
		printf("______________被删除同学的信息__________________________________\n");
		printf("|学号\t|姓名\t|性别\t|班级\t|年龄\t|备注\t|\n");
		printf("|%s\t|%s\t|%s\t|%s\t|%s\t|%s\t\n", data.id, data.name, data.surname, data.classs, data.age, data.note);
		printf("________________________________________________________________\n");
		break;
	case 5:
		
		printdLlist(L);
		
		break;
	case 6:
		save(&L);
		printdLlist(L);
		break;
	case 7:
		printf("欢迎再次使用该系统，若有不当的地方请谅解！！！\n");
		exit(0);
		break;
	default:
		break;
	}
	
	printf("是否继续使用该系统1/0\n");
	int chos = 0;
	scanf("%d", &chos);
	system("cls");
	if (chos == 1)goto hhhe;
	else printf("欢迎再次使用该系统\n");
}

else
{
	printf("欢迎下次光临\t");
}
}

void systeminto()
{
	printf("\t【系统简介】\t\n");
	printf("\t1.本系统致力于储存学生信息\t\n");
	printf("\t2.初次进入系统后，首先要录入信息\t\n");
	printf("\t3.每次录入完信息后，记得报 保 存\t\n");
	printf("\t【感谢你的使用】\t");

}
void Account_Password()
{
	
	int t = 0;
	char isAccount[20] = { "123456789" };
	char isPassword[20] = { "qwertyuiop" };
	char Account[20];
	char Password[20];
	
password:printf("请输入账号和密码\n");
	printf("账号:\n");
	scanf("%s", Account);
	printf("密码:\n");
	scanf("%s", Password);
	if (strcmp(Account, isAccount) == 0 && strcmp(Password, isPassword) == 0)
	{
		system("cls");
		munu();
		
	}
	else {
		printf("账号或密码错误，请重新输入\n");
		t++;
		if(t!=3)
		goto password;
		else {
			printf("您账号或密码输入错误已达三次，已自动退出系统，若想再次进入请需更改密码");
		}
	}
}
int main()
{
	system("TITLE 学生信息管理系统");
	initList(&L);
	read(&L);
	Account_Password();
	

	/*printdLlist(L);*/
	/*还需要添加功能：
	4.排序功能
	*/


}

