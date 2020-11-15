``` cpp
// https://www.programiz.com/cpp-programming/function-overriding


                                                                /* ----------------IMPORTANT---------------- */
// https://stackoverflow.com/questions/4937180/a-base-class-pointer-can-point-to-a-derived-class-object-why-is-the-vice-versa

/*-----------------------------------------------------------------------*/
#include <iostream>
using namespace std;

class Vehicle {
public :
	string color;

	void print() {
		cout << "Vehicle" << endl;
	}


};

class Car : public Vehicle {
public :
	int numGears;


	void print() {
		cout << "Car" << endl;
	}


};

int main() {
	Vehicle v;

	Car c;

	v.print();

	c.print();


	Vehicle *v1 = new Vehicle;

	Vehicle *v2;
	// v2 = &v;

	//base class pointer can point to derived class object as----
	//(it's basically base class object) bcs derived class is subclass of base class

	//vice-versa isnt possbiile

	v2 = &c;

	v1 -> print();

	v2 -> print();


}
```
