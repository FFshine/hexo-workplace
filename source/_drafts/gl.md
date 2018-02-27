---
title: 一个基于c++的很简单的成绩管理系统
tags:
  - c++
id: 897
categories:
  - 代码
date: 2018-01-05 16:31:02
---

* * *

#### 这是我花了一个晚上为室友×××写出来的简易的成绩管理系统。
```cpp
    /********************
     * 本实验在GUN/Linux下完成
     * 编译工具为gcc version 7.2.1
     * 不保证Windows/vc的兼容性
     *********************/

    #include&lt;iostream&gt;
    #include&lt;string&gt;
    #include&lt;unistd.h&gt;
    #include&lt;iomanip&gt;
    using namespace std;

    const int maxSize = 100;

    class Student{
        public:
            string name;
            long int number;
            float english;
            float chinese;
            Student(){}
    };

    class School{
        public:
            School(){}
            void setSchool(Student stu[], int n,int v){
                if(n&gt;maxSize)throw"错误";
                length = v;
                for(int i = 0;i&lt;n;i++){
                data[i] = stu[i];}
            }
            void insert(Student stu,int i){
                if(length&gt;=maxSize)throw"错误";
                if(i&lt;1||i&gt;length+1)throw"错误";
                for (int j = length;j&gt;=i;j--){
                data[j] = data[j-1];
                }
                data[i-1] = stu;
                length++;
            }
            string _delete(int i){
                if(length == 0)throw"错误";
                if(i&lt;1||i&gt;length)throw"错误";
                string x = data[i-1].name;
                for(int j = i;j&lt;length;j++){
                data[j-i] = data[j];}
                length--;int v = -1;
                return x;
            }
            void print(){
                cout&lt;&lt;setw(14)&lt;&lt;"学号"&lt;&lt;setw(14)&lt;&lt;"姓名"&lt;&lt;setw(14)&lt;&lt;"英语"&lt;&lt;setw(14)&lt;&lt;"语文"&lt;&lt;setw(14)&lt;&lt;"平均";
                for(int i = 0;i&lt;length;i++){
                    cout&lt;&lt;endl;
                    cout&lt;&lt;setw(12) &lt;&lt;data[i].number;
                    cout&lt;&lt;setw(12)&lt;&lt;data[i].name;
                    cout&lt;&lt;setw(12)&lt;&lt;data[i].english;
                    cout&lt;&lt;setw(12)&lt;&lt;data[i].chinese;
                    cout&lt;&lt;setw(12)&lt;&lt;(data[i].chinese+data[i].english)/2.0;
                    }
                    cout&lt;&lt;endl;
            }
            void searchByName(string name){
                for(int i = 0;i&lt;length;i++){
                    if(data[i].name == name)
                    {
                    cout&lt;&lt;"姓名:"&lt;&lt;data[i].name&lt;&lt;endl;
                    cout&lt;&lt;"学号:"&lt;&lt;data[i].number&lt;&lt;endl;
                    cout&lt;&lt;"英语:"&lt;&lt;data[i].english&lt;&lt;endl;
                    cout&lt;&lt;"语文:"&lt;&lt;data[i].chinese&lt;&lt;endl;
                    cout&lt;&lt;"平均:"&lt;&lt;(data[i].english+data[i].chinese)/2&lt;&lt;endl;
                    cout&lt;&lt;endl;
                    }
                }
            }
            int listByClass(string _class){
                float b[length];
                for(int i = 0;i&lt;length;i++){
                    if(_class == "英语"){
                        b[i] = data[i].english;
                    }
                    else if(_class == "语文"){
                        b[i] = data[i].chinese;
                    }
                    else if(_class == "平均"){
                        b[i] = (data[i].english+data[i].chinese)/2;
                    }
                    else{
                        cout&lt;&lt;"信息有误";
                        return 0;
                    }
                }
                //冒泡排序
                for(int i = 0;i&lt;length;i++){
                    for (int j = i + 1; j &lt; length; j++)
                    {
                        if (b[i] &gt; b[j]){
                            int c;
                            c = b[i];
                            b[i] = b[j];
                            b[j] = c;
                        }
                    }
                }
                for(int i = 0;i&lt;length;i++){
                    cout&lt;&lt;b[i]&lt;&lt;"  ";
                }
                cout&lt;&lt;endl;
                return 0;
            }
            void searchByInfo(string _info){
                if(_info == "语文"|| _info == "英语"||_info == "平均"){
                    listByClass(_info);
                }
                else searchByName(_info);
            }
        private:
            Student data[maxSize];
            int length;
    };

        void lead(){
        system("clear");
        cout&lt;&lt;endl&lt;&lt;endl&lt;&lt;endl;
        cout&lt;&lt;"************************************"&lt;&lt;endl;
        cout&lt;&lt;"*-------古月日华成绩管理系统-------*"&lt;&lt;endl;
        cout&lt;&lt;"************************************"&lt;&lt;endl;
        cout&lt;&lt;"**                                **"&lt;&lt;endl;
        cout&lt;&lt;"**  欢迎来到古月日华成绩管理系统  **"&lt;&lt;endl;
        cout&lt;&lt;"**  请选择操作(输入相应数字)      **"&lt;&lt;endl;
        cout&lt;&lt;"**  1\. 录入成绩                   **"&lt;&lt;endl;
        cout&lt;&lt;"**  2\. 输出成绩表                 **"&lt;&lt;endl;
        cout&lt;&lt;"**  3\. 插入学生成绩               **"&lt;&lt;endl;
        cout&lt;&lt;"**  4\. 删除某个学生成绩           **"&lt;&lt;endl;
        cout&lt;&lt;"**  5\. 根据关键字查找学生成绩     **"&lt;&lt;endl;
        cout&lt;&lt;"**  6\. 根据关键字排序             **"&lt;&lt;endl;
        cout&lt;&lt;"**  7\. 根据关键字筛选出数据       **"&lt;&lt;endl;
        cout&lt;&lt;"**  8\. 退出                       **"&lt;&lt;endl;
        }

    int main(){
        int i;
        Student stu[100];
        School a;
        int v = 0;
        lead();
        cin&gt;&gt;i;
        while(i!=8){
                switch(i){
                case 1:
                system("clear");
                while(1){
                char y = 'q';
                cout&lt;&lt;"请依次输入该生的以下信息："&lt;&lt;endl;
                cout&lt;&lt;"姓名：";
                string name;
                cin&gt;&gt;name;
                cout&lt;&lt;"学号：";
                long int number;
                cin&gt;&gt;number;
                cout&lt;&lt;"英语成绩：";
                float english;
                cin&gt;&gt;english;
                cout&lt;&lt;"语文成绩：";
                float chinese;
                cin&gt;&gt;chinese;
                cout&lt;&lt;"确认请输入 y，重输请输入 r，退出请输入 n：";
                cin&gt;&gt;y;
                if(y == 'y'){
                    cout&lt;&lt;"储存完成，是否继续输入,是请输入 y，退出请输入 n：";
                    stu[v].name = name;
                    stu[v].chinese = chinese;
                    stu[v].english = english;
                    stu[v].number = number;
                    v++;
                    char j;
                    cin &gt;&gt; j;
                    if(j == 'n'){
                    a.setSchool(stu,20,v);
                    cout&lt;&lt;"保存成功";
                    sleep(1);
                    system("clear");
                    break;
                    }
                }
                else if(y == 'r') continue;
                else if(y == 'n') {
                a.setSchool(stu,20,v);
                cout&lt;&lt;"保存成功";
                sleep(1);
                system("clear");
                break;}
                }
                break;
                case 2: {
                    system("clear");
                    a.print();
                cout&lt;&lt;endl&lt;&lt;"打印完成，输入exit退出"&lt;&lt;endl;
                string _class = "o";
                while(_class != "exit"){
                cin&gt;&gt;_class;
                }
                system("clear");
                break;}
                case 3: {
                system("clear");
                cout&lt;&lt;"请依次输入该生以下信息："&lt;&lt;endl;
                cout&lt;&lt;"姓名：";
                string name;
                cin&gt;&gt;name;
                cout&lt;&lt;"学号：";
                long int number;
                cin&gt;&gt;number;
                cout&lt;&lt;"英语成绩：";
                float english;
                cin&gt;&gt;english;
                cout&lt;&lt;"语文成绩：";
                float chinese;
                cin&gt;&gt;chinese;
                cout&lt;&lt;"插入位置：";
                int n;
                cin&gt;&gt;n;
                Student h;
                h.name = name;
                h.number = number;
                h.english = english;
                h.chinese = chinese;
                a.insert(h,i);
                cout&lt;&lt;endl&lt;&lt;"插入完成！输入exit返回总菜单："&lt;&lt;endl;
                while(name != "exit"){
                    cin&gt;&gt;name;
                }
                system("clear");
                break;
                }

                case 4:{
                system("clear");
                cout&lt;&lt;"请输入删除的位置：";
                int y;
                cin&gt;&gt;y;
                cout&lt;&lt;a._delete(y)&lt;&lt;"已经从系统中删除"&lt;&lt;endl;
                cout&lt;&lt;endl&lt;&lt;"输入exit退出"&lt;&lt;endl;
                string _class = "o";
                while(_class != "exit"){
                cin&gt;&gt;_class;
                }
                system("clear");
                break;
                }
                case 5:{
                    system("clear");
                    cout&lt;&lt;"请输入要查找的姓名：";
                    string name;
                    cin&gt;&gt;name;
                    a.searchByName(name);
                    cout&lt;&lt;endl&lt;&lt;"输入exit退出"&lt;&lt;endl;
                    while(name != "exit"){
                        cin&gt;&gt;name;
                    }
                    system("clear");
                    break;
                }
                case 6:{
                    system("clear");
                    cout&lt;&lt;"请输入您要查找的科目：";
                    string _class;
                    cin&gt;&gt;_class;
                    cout&lt;&lt;"我们找到如下结果：";
                    a.listByClass(_class);
                    cout&lt;&lt;endl&lt;&lt;"输入exit退出"&lt;&lt;endl;
                    while(_class != "exit"){
                        cin&gt;&gt;_class;
                    }
                    system("clear");
                    break;
                }

                case 7:{
                    system("clear");
                    cout&lt;&lt;"请输入您要查找的信息（科目、姓名、平均）";
                    string _info;
                    cin&gt;&gt;_info;
                    a.searchByInfo(_info);
                    cout&lt;&lt;endl&lt;&lt;"输入exit退出"&lt;&lt;endl;
                    while(_info != "exit"){
                        cin&gt;&gt;_info;
                    }
                    system("clear");
                    break;
                }
                default:{
                system("clear");
                cout&lt;&lt;"输入有误,请重新选择"&lt;&lt;endl;sleep(1);
                system("clear");
                break;}
            }
            lead();
            cin&gt;&gt;i;
        }
        return 0;
    }
```