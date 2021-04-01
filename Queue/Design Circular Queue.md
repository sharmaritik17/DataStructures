https://leetcode.com/problems/design-circular-queue/


https://leetcode.com/problems/design-circular-queue/discuss/1137859/Unique-approach-Straight-forward-90-faster-Easy-buzzy

``` 
class MyCircularQueue {
    int *data;
    int frontIndex;
    int nextIndex;
    int size;
    int capacity;
public:
    MyCircularQueue(int s) {
        data = new int[s];
        frontIndex = -1;
        nextIndex = 0;
        size = 0;
        capacity = s;
    }

    bool isFull() {
        return size == capacity;
    }

    bool isEmpty() {
        return size == 0;
    }

    bool enQueue(int element) {
        if (isFull()) {
             return 0;
        }

        data[nextIndex] = element;
        nextIndex = (nextIndex + 1) % capacity;
        if (frontIndex == -1) {
            frontIndex = 0;
        }
        size++;
        return 1;
    }

    int Front() {
        if (isEmpty())
            return -1;

        return data[frontIndex];
    }
	
    int Rear() {
        if (isEmpty())
            return -1;

      int index = (nextIndex - 1 + capacity)%capacity;
      return data[index];
    }    

    bool deQueue() {
        if (isEmpty())
            return 0;

        frontIndex = (frontIndex + 1) % capacity;
        size--;
        
        return 1;
    }

};
