``` cpp
//https://leetcode.com/playground/H4ocKj22/live

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/

#include  <bits/stdc++.h>
#define MAX 1000
#define mod     1000000009
#define FIO     ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define nul     NULL
#define hell    INT_MIN
#define hevn    INT_MAX
#define ll     long long
#define  z "\n"
#include <iostream>
#include <vector>
#include <climits>
#define ff first
#define ss second
using namespace std;

/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/

class Vehicle {
private:
	int maxSpeed;
protected:
	int numTyres;
public:
	string color;

	Vehicle() {
		cout << "Vehicle default constructor" << endl;
	}

	~Vehicle() {
		cout << "Vehicle destructor" << endl;
	}
};

class Car: public Vehicle {
public:
	int numGears;
	
//here first call goes to parent class explicitily will be Car():Vechicle() ------intialization list

	Car() {
		cout << "Car default constructor" << endl;
	}
	
 // if we want to call parent paramterized constructor Car(int x):Vehicle(x)
    //it's must to call parent param... if parent default isnt available
    
	~Car() {
		cout << "Car destructor" << endl;
	}
};

class HondaCity: public Car{
public:

	HondaCity(){
		cout << "HondaCity default constructor" << endl;
	}

	~HondaCity(){
		cout << "HondaCity destructor" << endl;
	}
};

int main() {
// 	/* -----------------------------------------------------------------------*/
// #ifndef ONLINE_JUDGE
// 	freopen("input.txt", "r", stdin);
// 	freopen("output.txt", "w", stdout);
// #endif
// 	/* -----------------------------------------------------------------------*/
	Vehicle v;

	v.color = "BLUE";
	//v.numTyres = 10;  //only accessible by derived class

	Car c;
	c.color = "BLACK";
	c.numGears = 17;
    
       HondaCity hc;
}
```
