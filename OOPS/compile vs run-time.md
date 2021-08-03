https://www.javatpoint.com/cpp-virtual-function
``` cpp

/*
overloading 
*/

/* COMPILE TIME ONLY*/
#include<iostream>
using namespace std;

int add(float x,float y,int z){
    return x+y+z;
}
int add(int x,int y){
    return x+y;
}
int main(){
    cout<<add(1,2)<<endl;
    cout<<add(1.0,3.0,8)<<endl;
    return 0;
}


/*BOTH BE DONE COMPILE AND RUN TIME BUT RUN TIME THAT'S WE NEEDED EVERYWHERE*/
/*
overriding
*/

#include<iostream>
using namespace std;

class Parent{
    public:
    int no_children;
    Parent(){
       no_children=0; 
    }
    virtual void myStrength(){ /* with the help of it's running on run-time*/
        cout<<"I'm Parent and My Strengths are as follows:"<<endl;
    }
   void display(){ /* without the help of it's running on compile-time*/
        cout<<"I'm good to be old"<<endl;
    }
};

class Child : public Parent{
    public:
    void myStrength(){
        cout<<"I'm Child and My Strengths are as follows:"<<endl;
    }
    void display(){
        cout<<"I'm good to be young"<<endl;
    }
};

int main(){
    Parent *par;
    Child child;
    par = &child;
    par->myStrength();
    par->display();
}

/*
pure vivrtual function
*/

#include<iostream>
using namespace std;

class Parent{
    public:
    int no_children;
    Parent(){
       no_children=0; 
    }
    virtual void display_toys()=0;
};

class Child : public Parent{
    public:
    void display_toys(){
        cout<<"I'm Child and I have truck/car/monkey"<<endl;
    }
    void display(){
        cout<<"I'm good to be young"<<endl;
    }
};

int main(){
    Parent *par;
    Child child;
    par = &child;
    par->display_toys();
    /*base class pointer points to derived class object and we want this functionailty because we want to access all things of dervied class explicilty without informing it.
    */
}
