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

------------------------------------------------------------------------------------------------------------------------------------
## 1. C++ 11 Introduction ##

## 2. Initializer List ##

  It is used to mainly initialize the variables of the class and it can initialize only part of the variables.

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
