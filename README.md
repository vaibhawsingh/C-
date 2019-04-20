# C++ 11

This Documents will explains alomst all the C++ 11 concepts from zero level to advanced level. Every Chapter in this tutorials explains the concepts with appropriate code snippet and for detailed source code visit the Source of Repository.

-------------------------------------------------------------------------------------------------------------------------------

[1. C++ 11 Introduction](#1-c++-11-intorduction)

[2. Initializer List](#2-initializer-list)

[3. Static Assertion](#3-static-assertion)

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
</pre></code>
