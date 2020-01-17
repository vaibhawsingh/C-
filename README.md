# C++ 11

This Documents will explains alomst all the C++ 11 concepts from zero level to advanced level. Every Chapter in this tutorials explains the concepts with appropriate code snippet and for detailed source code visit the Source of Repository.

-------------------------------------------------------------------------------------------------------------------------------

[1. C++ 11 Introduction](#1-c++-11-intorduction)

[2. Initializer List](#2-initializer-list)

[3. Static Assertion](#3-static-assertion)

[4. Variadic Function](#4-variadic-function)

[5. Virtual Constructor](#5-virtual-constructor)

[6. Std Thread](#6-std-thread)

[7. Class vs Struct](#7-class-vs-struct)

[8. Access Specifiers](#8-access-specifiers)

[9. Const in C++](#8-const-in-c++)

------------------------------------------------------------------------------------------------------------------------------------
## 1. C++ 11 Introduction ##

## 2. Initializer List ##

  It is used to mainly initialize the variables of the class and it can initialize only part of the variables.
   ### For initialization of non-static const data members ###
<pre><code>
class Test { 
    const int t; 
public: 
    Test(int t):t(t) {}  //Initializer list must be used 
    int getT() { return t; } 
}; 
</code></pre>
   ### For initialization of reference members ###
<pre><code>
class Test 
{ 
    int &t; 
public: 
    Test(int &t):t(t) {}  //Initializer list must be used 
    int getT() { return t; } 
}; 
</code></pre>
   ### For initialization of member objects which do not have default constructor ### 
<pre><code>
class A { 
    int i; 
public: 
    A(int ); 
}; 
  
A::A(int arg) { 
    i = arg; 
    cout << "A's Constructor called: Value of i: " << i << endl; 
} 
  
// Class B contains object of A 
class B { 
    A a; 
public: 
    B(int ); 
}; 
  
B::B(int x):a(x) {  //Initializer list must be used 
    cout << "B's Constructor called"; 
} 
</code></pre>
If class A had both default and parameterized constructors, then Initializer List is not must if we want to initialize “a” using default constructor, but it is must to initialize “a” using parameterized constructor.
  ### For initialization of base class members ###
<pre><code>
class A { 
    int i; 
public: 
    A(int ); 
}; 
  
A::A(int arg) { 
    i = arg; 
    cout << "A's Constructor called: Value of i: " << i << endl; 
} 
  
// Class B is derived from A 
class B: A { 
public: 
    B(int ); 
}; 
  
B::B(int x):A(x) { //Initializer list must be used 
    cout << "B's Constructor called"; 
}
</code></pre>
   ### When constructor’s parameter name is same as data member ###
<pre><code>
class A { 
    int i; 
public: 
    A(int ); 
    int getI() const { return i; } 
}; 
  
A::A(int i):i(i) { }  // Either Initializer list or this pointer must be used 
/* The above constructor can also be written as  
A::A(int i) {  
    this->i = i; 
} 
*/
</code></pre>
   ### For Performance reasons ###
<pre><code>
// Without Initializer List 
class MyClass { 
    Type variable; 
public: 
    MyClass(Type a) {  // Assume that Type is an already 
                     // declared class and it has appropriate  
                     // constructors and operators 
      variable = a; // assignment operator function called
    } 
}; 

// With Initializer List 
class MyClass { 
    Type variable; 
public: 
    MyClass(Type a):variable(a) {   // Assume that Type is an already 
                     // declared class and it has appropriate 
                     // constructors and operators 
		     //No assignment operator function called
    } 
}; 
</code></pre>

## 3. Static Assertion ##
  static_assert function is used for checking the correctness of code.
<pre><code>
#include &lt;type_traits&gt;
using namespace std;
template< typename T, typename U>
auto add(T t, U u)
{
	static_assert(is_integral&lt;T&gt;::value, "first value must be integral ");

	return t + u;
}

int main()
{
	add("JMV", 5);
    return 0;
}
</code></pre>

## 4. Variadic Function ##
   This function template is used for taking n number of variable.
   
<pre><code>

using namespace std;
auto add() { return 0; }
template< typename H, typename... T>
auto add(H h, T... t)
{
	return h + add(t...);
}

int main()
{
	add("JMV", 5,4);
    return 0;
}
</code></pre>

### Another Example ###
	
<pre><code>
using namespace std;
auto sum_product(double a, double b)
{
	return make_pair(a+b, a*b);
}
int main()
{
    //old way
    auto val = sum_product(3,4);
    auto s = get&lt;0&gt;(val);
    //c++ 11
    float s;
    tie(s,ignore) = sum_product(3,4);
    return 0;
}
</code></pre>

## 5. Virtual Constructor ##

In C++ we can not have the virtual constructor. virtual comes into the picture when we call derived class function using base class pointer to derived class object. when a constructor of a class is executed there is no virtual table in the memory, means no virtual pointer defined yet. hence virtual constructor is not possible.

## 6. Std Thread ##

In c++11 thread is a class and it can be used as object. It can be created in 2 ways.
<pre><code>
std::thread threadObj(function);
std::thread([&]() {this->MemberFuncion(parameter);}).detach();
</code></pre>

## 7. Class vs Struct ##

|    Class	|    Struct	|
| ------------- | ------------- |
| private by default  | public by default  |

Apart from this there is no difference. struct can be used for accumulating data types where as class can be used for object in real world.

## 8. Access Specifiers ##

| Base class Component	|  Class Inherited as  | Resulting access inside the subclass |
| ------------- | ------------- | ----------- |
| public <td rowspan=3>public  | public |
| protected   | protected |
| private	| none |
| public <td rowspan=3>protected  | protected |
| protected   | protected |
| private	| none |
| public <td rowspan=3>private  | private |
| protected   | private |
| private	| none |

## 9. Const in C++ ##
   ### Function overloading and const keyword ###
<pre><code>

//Member function overloading Example
class Test 
{ 
protected: 
    int x; 
public: 
    Test (int i):x(i) { } 
    void fun() const //called by const object
    { 
        cout << "fun() const called " << endl; 
    } 
    void fun() //called by non-const object
    { 
        cout << "fun() called " << endl; 
    } 
}; 
</code></pre>
<pre><code>
// PROGRAM 1 (Fails in compilation) bcz pass by value
void fun(const int i) 
{ 
    cout << "fun(const int) called "; 
} 
void fun(int i) 
{ 
    cout << "fun(int ) called " ; 
} 
int main() 
{ 
    const int i = 10; 
    fun(i); 
    return 0; 
} 
</code></pre>
<pre><code>
// PROGRAM 2 (Compiles and runs fine) 
void fun(char *a) 
{ 
  cout << "non-const fun() " << a; 
} 
  
void fun(const char *a) 
{ 
  cout << "const fun() " << a; 
} 
  
int main() 
{ 
  const char *ptr = "GeeksforGeeks"; 
  fun(ptr); 
  return 0; 
} 
</code></pre>
<pre><code>
// PROGRAM 3 (Compiles and runs fine)
void fun(const int &i) 
{ 
    cout << "fun(const int &) called "; 
} 
void fun(int &i) 
{ 
    cout << "fun(int &) called " ; 
} 
int main() 
{ 
    const int i = 10; 
    fun(i); 
    return 0; 
} 
</code></pre>
C++ allows functions to be overloaded on the basis of const-ness of parameters only if the const parameter is a reference or a pointer.
