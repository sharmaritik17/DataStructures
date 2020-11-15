https://practice.geeksforgeeks.org/problems/circular-tour/1#

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/
``` cpp
int tour(petrolPump p[], int n)
{
    //Your code her
    int capacity = 0;
    int broken_capacity = 0;
    int start = 0;
    for (int i = 0; i < n;i++) {
        capacity += p[i].petrol - p[i].distance;
        if (capacity < 0) {
            broken_capacity += capacity;
            start = i + 1;
            capacity = 0;
        }
    }

    return (broken_capacity + capacity > 0) ? start : -1;
}
```
