---
layout: post
title:  Data Structures and Algorithm
date:   2024-03-17 09:29:20 +0700
tags: [dsa]
categories: jekyll update
usemathjax: true
---

I am following [Strivers A2Z DSA Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) containing 455 problems. You can find my Github repository for [DSA](https://github.com/ksamaarora/DSA) and [LeetCode](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbVc2aXgtYXE4VGp1MkVvT0MxLWNNYjE3M1J1d3xBQ3Jtc0ttdnVseFhwS1VueE0zVlFCTnFIb1BCbWJVbjVCTjYtOXBBalg4bWk3SU1TVFE1cGZ3Y2E2Ui1YUUpXU2JPNnhURVpMTkNkeUQ1UHFDWjlIVDI2Z2UzTnZZSzBMWjNISjEycWpZamtxYU1tYndkTS1rVQ&q=https%3A%2F%2Fdocs.google.com%2Fspreadsheets%2Fd%2F1-wKcV99KtO91dXdPkwmXGTdtyxAfk1mbPXQg81R9sFE%2Fedit%3Fusp%3Dsharing&v=NXQi_g1pVqI) here. 

> Below are a few sums i solved in leetcode.
- [0001-two-sum](https://github.com/ksamaarora/LeetCode/tree/main/0001-two-sum)
- [0334-increasing-triplet-subsequence](https://github.com/ksamaarora/LeetCode/tree/main/0334-increasing-triplet-subsequence)
- [0345-reverse-vowels-of-a-string](https://github.com/ksamaarora/LeetCode/tree/main/0345-reverse-vowels-of-a-string)
- [0605-can-place-flowers](https://github.com/ksamaarora/LeetCode/tree/main/0605-can-place-flowers)
- [1431-kids-with-the-greatest-number-of-candies](https://github.com/ksamaarora/LeetCode/tree/main/1431-kids-with-the-greatest-number-of-candies)
- [1768-merge-strings-alternately](https://github.com/ksamaarora/LeetCode/tree/main/1768-merge-strings-alternately)
- [2390-removing-stars-from-a-string](https://github.com/ksamaarora/LeetCode/tree/main/2390-removing-stars-from-a-string)
- [0007-reverse-integer](https://github.com/ksamaarora/LeetCode/tree/main/0007-reverse-integer)
- [0009-pallindrome-number](https://github.com/ksamaarora/LeetCode/tree/main/0009-palindrome-number)
- [0013-roman-to-integer](https://github.com/ksamaarora/LeetCode/tree/main/0013-roman-to-integer)


C++ Basics in One Shot - Strivers A2Z DSA Course - L1

A) BASIC I/O.

```
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
C) IF ELSE 	
```
// write a program that takes input of age 
	// and prints if you are adult or not 
	#include<iostream>
	using namespace std;
	int main(){
	    int age;
	    cin>>age;
	    if(age>=18){
	        cout<<"Adult";
	    }
	    else{
	        cout<<"Not Adult";
	    }
	    return 0;
	}
```	
Nested If Else 

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



	D) SWITCH
	
	// Take the day no. and print the corresponding day 
	// for 1 print Monday, 2 print Tuesday and so on
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
	
	
	
	E) ARRAYS
	In arrays we have zero-based indexing. 
	
	
	
	
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
	
	
	
	2D Array
	
	
	
	#include<iostream>
	using namespace std;
	int main(){
	    int arr[3][5];
	    arr[1][3]=70;
	    cout<<arr[1][3];
	    return 0;
	}
	
	
	F) STRINGS
	
	#include<iostream>
	using namespace std;
	int main(){
	    string s="ksama";
	    cout<<s[3]<<endl;
	    int len=s.size();
	    cout<<s[len-1];
	    return 0;
	}
	
	
	
	G) FOR LOOP
	
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
	
	
	H) WHILE LOOP
	
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
	
	I) DO WHILE LOOP
	
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
	
	
	J) FUNCTIONS
	
	
	// Functions can be:
	// void - does not return anything
	// return
	// parameterized
	// non parameterized
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
	
	
	
	// In-built functions - min max
	#include<iostream>
	using namespace std;
	int main(){
	    int a,b;
	    cin>>a>>b;
	    cout<<min(a,b)<<endl;
	    cout<<max(a,b);
	    return 0;
	}
	
	
	K) PASS BY VALUE AND REFERENCE 
	

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


NOTE: ARRAY ALWAYS GOES BY PASS BY REFERENCE - Any changes made to the array using a function would make changes in the original array 


<!-- ### RECURSION

### DYNAMIC PROGRAMMING

### STRINGS

### MATHS

#### GREEDY

### DFS

### TREE

### HASH TABLE

### BINARY SEARCH

### BFS

### TWO POINTER

### STACK

### DESIGN

### GRAPH

### BIT MANIPULATION

### LINKED LIST

### HEAP

### SLIDING WINDOW

### TREE

### SEGMENT TREE -->
