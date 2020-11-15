``` cpp
 // https://www.programiz.com/cpp-programming/friend-function-class
 
 class Bus {
public:
	void print();
};

void test();

class Vehicle {
private:
	int x;
public:
	int y;
protected:
	int z;
        
	// Bus is friend of vehicle, can access private things of vehicle // even inside bus class 
	// vehicle may not be friend of bus but here bus is friend of vehicle only
	friend class Bus;

	friend void test();
};

void Bus::print() {
	Vehicle v1;
	v1.x = 10;
	v1.y = 15;
	cout << v1.x << " " << v1.y << endl;
}

void test() {
	Vehicle v1;
	v1.x = 100;
	v1.y = 150;
	cout << v1.x << " " << v1.y << endl;
}

int main() {
	Bus b1;
	b1.print();
	test();
}
```
