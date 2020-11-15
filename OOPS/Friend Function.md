``` cpp

// https://www.programiz.com/cpp-programming/friend-function-class
// https://www.geeksforgeeks.org/friend-class-function-cpp/


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

	friend void Bus::print(); // Bus is friend of vehicle ....  Vehicle may not be friend of Bus one side friendship(not mutual)

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
