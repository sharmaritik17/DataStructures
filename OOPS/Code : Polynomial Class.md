``` cpp

/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/   MAIN CODE
#include <vector>
#include <climits>
#include <iostream>
using namespace std;
#include "Solution.h"



//Driver program to test above functions
int main()
{
    int count1,count2,choice;
    cin >> count1;
    
    int *degree1 = new int[count1];
    int *coeff1 = new int[count1];
    
    for(int i=0;i < count1; i++) {
        cin >> degree1[i];
    }
    
    for(int i=0;i < count1; i++) {
        cin >> coeff1[i];
    }
    
    Polynomial first;
    for(int i = 0; i < count1; i++){
        first.setCoefficient(degree1[i],coeff1[i]);
    }
    
    cin >> count2;
    
    int *degree2 = new int[count2];
    int *coeff2 = new int[count2];
    
    for(int i=0;i < count2; i++) {
        cin >> degree2[i];
    }
    
    for(int i=0;i < count2; i++) {
        cin >> coeff2[i];
    }
    
    Polynomial second;
    for(int i = 0; i < count2; i++){
        second.setCoefficient(degree2[i],coeff2[i]);
    }
    
    cin >> choice;
    
    switch(choice){
            // Add
        case 1:
        {
            Polynomial result1 = first + second;
            result1.print();
            break;
        }
            // Subtract
        case 2 :
        {
            Polynomial result2 = first - second;
            result2.print();
            break;
        }
            // Multiply
        case 3 :
        {
            Polynomial result3 = first * second;
            result3.print();
            break;
        }
        case 4 : // Copy constructor
        {
            Polynomial third(first);
            if(third.degCoeff == first.degCoeff) {
                cout << "false" << endl;
            }
            else {
                cout << "true" << endl;
            }
            break;
        }
            
        case 5 : // Copy assignment operator
        {
            Polynomial fourth(first);
            if(fourth.degCoeff == first.degCoeff) {
                cout << "false" << endl;
            }
            else {
                cout << "true" << endl;
            }
            break;
        }
            
    }
    
    return 0;
}

/*++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*/ IMPLEMENTED CODE

class Polynomial {
public:
    int *degCoeff;
    int capacity;

// default constructor
    Polynomial() {
        degCoeff = new int[2];
        capacity = 2;
        for (int i = 0; i < 2; i++)
            degCoeff[i] = 0;
    }
// copy constructor
    Polynomial(Polynomial const &p) {
        this->capacity = p.capacity;
        this->degCoeff = new int [p.capacity];
        for (int i = 0; i < p.capacity; i++) {
            this->degCoeff[i] = p.degCoeff[i];
        }
    }
// set coefficient
    void setCoefficient(int degree, int coefficient) {
        if (degree >= capacity) {
            int size = 2 * capacity;
            while (degree >= size) {
                size = 2 * size;
            }
            int *new_arr = new int[size];
            for (int i = 0; i < size; i++) {
                new_arr[i]  = 0;
            }
            for (int i = 0; i < capacity; ++i)
            {
                new_arr[i] = degCoeff[i];
            }
            delete [] degCoeff;
            degCoeff = new_arr;
            capacity = size;
        }
        degCoeff[degree] = coefficient;
    }
// overload + operator
    Polynomial operator+(Polynomial const &p) const {
        Polynomial pnew;
        int start_this = 0;
        int start_passed = 0;
        while (start_this < this->capacity && start_passed < p.capacity) {
            pnew.setCoefficient(start_this, degCoeff[start_this] + p.degCoeff[start_passed]);
            start_this++;
            start_passed++;
        }
        while (start_this < this->capacity) {
            pnew.setCoefficient(start_this, degCoeff[start_this]);
            start_this++;
        }
        while (start_passed < p.capacity) {
            pnew.setCoefficient(start_passed, p.degCoeff[start_passed]);
            start_passed++;
        }
        return pnew;
    }
// overload - operator
    Polynomial operator-(Polynomial const &p) const {
        Polynomial pnew;
        int start_this = 0;
        int start_passed = 0;
        while (start_this < this->capacity && start_passed < p.capacity) {
            pnew.setCoefficient(start_this, degCoeff[start_this] - p.degCoeff[start_passed]);
            start_this++;
            start_passed++;
        }
        while (start_this < this->capacity) {
            pnew.setCoefficient(start_this, degCoeff[start_this]);
            start_this++;
        }
        while (start_passed < p.capacity) {
            pnew.setCoefficient(start_passed, (-1)*p.degCoeff[start_passed]);
            start_passed++;
        }
        return pnew;
    }
// to get coefficient for multiplication
    int getCoefficient(int degree) {
        if (degree >= capacity) {
            return 0;
        }
        return degCoeff[degree];
    }
// overload * operator
    Polynomial operator*(Polynomial const &p) const {
        Polynomial pnew;
        for (int i = 0; i < capacity; i++) {
            if (degCoeff[i]) {
                for (int j = 0; j < p.capacity; j++) {
                    if (p.degCoeff[j]) {
                        int mul = degCoeff[i] * p.degCoeff[j];
                        int sum = pnew.getCoefficient(i + j) + mul;
                        pnew.setCoefficient(i + j, sum);
                    }
                }
            }
        }
        return pnew;
    }
// copy assignment operator =
    void operator=(Polynomial const &p) {
        capacity = p.capacity;
        degCoeff = new int[p.capacity];
        for (int i = 0; i < p.capacity; i++) {
            degCoeff[i] = p.degCoeff[i];
        }
    }
// print function
    void print() const {
        for (int i = 0; i < capacity; i++) {
            if (degCoeff[i]) {
                cout << degCoeff[i] << "x" << i << " ";
            }
        }
        cout << endl;
    }

};
