---
layout: default
title: C++ Basics
---

A) BASIC I/O

```c++
#include<iostream>
using namespace std;
int main(){
    int x, y;
    cout<<"Demo"<<"\n";
    cout<<"Test"<<endl;
    cin>>x>>y;
    cout<<"Value of x is "<<x<<" Value of y is "<<y;
    return 0;
}
```

B) DATA TYPES

[![Screenshot-2024-05-10-at-6-19-52-PM.png](https://i.postimg.cc/W3BgsG5j/Screenshot-2024-05-10-at-6-19-52-PM.png)](https://postimg.cc/BLCXgKWw)

C) IF ELSE 	

```c++
// Check leap year using nested if-else
// A year is a leap year if it follows the condition, the year should be evenly divisible by 4 then the year should be evenly divisible by 100 then lastly year should evenly divisible by 400 otherwise the year is not a leap year. 
#include<iostream>
using namespace std;
int main(){
    int year;
    cin >> year;
    if(year % 4 == 0){
        if(year % 100 == 0){
            if(year % 400 == 0){
                cout << "It is a leap year";
            }
            else{
                cout << "It is not a leap year";
            }
        }
        else{
            cout << "It is a leap year";
        }
    }
    else{
        cout << "It is not a leap year";
    }
    return 0;
}
```

D) SWITCH

```c++
// Take the day no. and print the corresponding day for 1 print Monday, 2 print Tuesday and so on
#include<iostream>
using namespace std;
int main(){
	int day;
	cin>>day;
	switch(day){
	    case 1:
	    cout<<"Monday";
	    break;
	    case 2:
	    cout<<"Tuesday";
	    break;
	    case 3:
	    cout<<"Wednesday";
	    break;
	    case 4:
	    cout<<"Thursday";
	    break;
	    case 5:
	    cout<<"Friday";
	    break;
	    case 6:
	    cout<<"Saturday";
	    break;
	    case 7:
	    cout<<"Sunday";
	    break;
	    default:
	    cout<<"Invalid";
	}
	return 0;
}
```

E) ARRAYS: In arrays we have zero-based indexing. 

- 1D Array
```c++
#include<iostream>
#include<vector>
using namespace std;
int main(){
	int n;
	cin >> n;
	vector<int> arr(n); // Create a vector of size n
	    
	for(int i = 0; i < n; i++){
	    cin >> arr[i];
	}
	for(int i = 0; i < n; i++){
	    cout << arr[i] << " ";
	}
	return 0;
}
```

- 2D Array
```c++
#include<iostream>
using namespace std;
int main(){
	int arr[3][5];
	arr[1][3]=70;
	cout<<arr[1][3];
	return 0;
}
```

F) STRINGS

```c++
#include<iostream>
using namespace std;
int main(){
	string s="ksama";
	cout<<s[3]<<endl;
	int len=s.size();
	cout<<s[len-1];
	return 0;
}
```

G) FOR LOOP

```c++
#include<iostream>
using namespace std;
int main(){
	int i;
	for(i=1; i<=25; i=i+5){
	    cout<<"Ksama"<<i<<endl;
	}
	cout<<i;
	return 0;
}
```

H) WHILE LOOP

```c++
#include<iostream>
using namespace std;
int main(){
	int i=1; // Initialization
	while(i<=25){ // Condition
	    cout<<"Ksama"<<i<<endl;
	    i=i+5; // Increment
	}
	cout<<i<<endl;
	return 0;
}
```

I) DO WHILE LOOP

```c++
#include<iostream>
using namespace std;
int main(){
	int i=2;
	do{
	    cout<<"Ksama"<<i<<endl;
	    i=i+5;
	}while(i<=1);
	cout<<i<<endl;
	return 0;
}
```

J) FUNCTIONS: void, return, parameterized, non parameterized

```c++
#include<iostream>
using namespace std;
// void
void printName(){
	cout<<"Ksama"<<endl;
}
// void with parameters
void printNameparameter(string name){
	cout<<"Name is "<<name<<endl;
}
int main(){
	printName();
	string name;
	cin>>name;
	printNameparameter(name);
	return 0;
}
```

```c++
// Take two numbers and print its sum
#include<iostream>
using namespace std;
int sum(void){
	return 3+5;
}
int parametersum(int a, int b){
	return a+b;
}
int main(){
	cout<<sum()<<endl;
	int a,b;
	cin>>a>>b;
	cout<<parametersum(a,b);
	return 0;
}
```
// In-built functions - min max
```c++
min(a,b)
max(a,b)
```

K) PASS BY VALUE AND REFERENCE 

```c++
#include<iostream>
using namespace std;
// pass by value
void doSomething(int num){
    cout<<num<<endl;
    num+=5;
    cout<<num<<endl;
    num+=5;
    cout<<num<<endl;
    num+=5;
}
// pass by reference (& address)
void doSomethingelse(int &num){
    cout<<num<<endl;
    num+=5;
    cout<<num<<endl;
    num+=5;
    cout<<num<<endl;
    num+=5;
}
int main(){
    int num=10;
    doSomething(num);
    cout<<num<<endl;
    // NOTE: The final value of cout<<num is 10 beccause when the function gets called a copy is sent and not the original num 10 - it deals with the copy of num value 
    doSomethingelse(num);
    cout<<num;
    // NOTE: The final value has now changed according to the function because it takes the parameter value from the address of the num variable "&num" - it deals with the original num value 
    return 0;
}
```

- NOTE: ARRAY ALWAYS GOES BY PASS BY REFERENCE - Any changes made to the array using a function would make changes in the original array 