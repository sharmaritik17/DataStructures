``` cpp
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
#include "ComplexNumbers.h"
/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/


template<typename T>
class Node {
public:
    T data;
    Node<T> *next;


    Node(T element) {
        data = element;
        next = NULL;
    }

};

template<typename T>
class QueueUsingLL {
    Node<T> *head;
    Node<T> *tail;
    int size;

public:
    QueueUsingLL() {
        head = NULL;
        tail = NULL;
        size = 0;
    }

    int getSize() {
        return size;
    }

    bool isEmpty() {
        return size == 0;
    }

    void enqueue(T element) {
        Node<T> *newNode = new Node<T>(element);
        if (head == nul) {
            head = newNode;
            tail = newNode;
        }
        else {
            tail->next = newNode;
            tail = newNode;
        }
        size++;
    }

    T front() {
        if (isEmpty())
            return hell;

        return head->data;
    }

    T dequeue() {
        if (isEmpty())
            return hell;

        Node<T> *remove;
        T save_data = head->data;
        remove = head;
        head = head->next;
        delete remove;
        size--;

        return save_data;
    }

};


int main() {
	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/

	QueueUsingLL<int> q;

	q.enqueue(10);
	q.enqueue(20);
	q.enqueue(30);
	q.enqueue(40);
	q.enqueue(50);
	q.enqueue(60);


	cout << q.front() << endl;
	cout << q.dequeue() << endl;
	cout << q.dequeue() << endl;
	cout << q.dequeue() << endl;

	cout << q.getSize() << endl;
	cout << q.isEmpty() << endl;
	cout << q.dequeue() << endl;
	cout << q.dequeue() << endl;
	cout << q.dequeue() << endl;
	cout << q.dequeue() << endl;
	cout << q.dequeue() << endl;
	cout << q.dequeue() << endl;


	/*||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||*/
	return 0;
}
