
``` cpp
//stack by using array
template<typename T>
//stack implementation using array
class stack_Using_Array {
    T *data;
    int nextIndex;
    int capacity;

public:
    stack_Using_Array() {
        data = new T[4];
        capacity = 4;
        nextIndex = 0;
    }

    bool is_empty() {
        return nextIndex == 0;
    }

    int size() {
        return nextIndex;
    }

    void push(T element) {
        // dynamic array for stack
        if (nextIndex == capacity) {
            T *new_data = new T[2 * capacity];
            for (int i = 0; i < capacity; i++) {
                new_data[i] = data[i];
            }
            capacity *= 2;
            delete [] data;
            data = new_data;
        }
        data[nextIndex] = element;
        nextIndex++;
    }

    T pop() {
        if (nextIndex == 0) {
            cout << "stack is empty\n";
            return 0;
        }
        nextIndex--;
        return data[nextIndex];
    }

    T top() {
        if (nextIndex == 0) {
            cout << "stack is empty\n";
            return 0;
        }
        return data[nextIndex - 1];
    }

};

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/
int main() {
	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/

	stack_Using_Array<char> s;
	s.push(100);
	s.push(101);
	s.push(102);
	s.push(103);
	s.push(104);

	cout << s.top() << z;
	cout << s.top() << z;

	s.pop();
	cout << s.top() << z;

	cout << s.size() << z;
	cout << s.is_empty() << z;


	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/
	return 0;
}
