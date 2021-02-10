 ``` cpp
 // stack by using linked list
template<typename T>
class Node {
public:
    T data;
    Node <T> *next;

    Node(T data) {
        this->data = data;
        next = NULL;
    }
};
template<typename T>
class stack_using_ll {
    Node <T> *head;
    int size;
public:
    stack_using_ll() {
        head = NULL;
        size = 0;
    }

    int get_size() {
        return size;
    }

    bool is_empty() {
        return size == 0;
    }

    void push(T element) {
        Node<T> *newNode = new Node<T>(element);
        if (head == NULL) {
            head = newNode;
        }
        else {
            newNode->next = head;
            head = newNode;
        }
        size++;
    }

    T pop() {
        if (!size)
            return 0;
        Node<T> *remove = NULL;
        remove = head;
        T save_data = head->data;
        head = head->next;
        delete(remove);
        size--;
        return save_data;
    }

    T top() {
        if (!size)
            return 0;
        return head->data;
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
