---
layout: post
title: "Interview questions - programming"
date: 2012-09-02 19:37
comments: true
keywords: "interview questions, software engineer interview, java interview"
categories: Jogging
---

Tomorrow will be my first day of my new job. After graduation, I have gone through quite a large number of articles regarding interview questions and programming tricks. I am gonna list some interesting ones.

1. Check if at least 2 out of 3 booleans is true
----- 

This one come from [StackOverflow](http://stackoverflow.com/questions/3076078/check-if-at-least-2-out-of-3-booleans-is-true). I like to solve simple problem in one line which is:
    return a ?(b || c):(b && c);
or
    return a &&(b || c)||(b && c);
or, here is some awesomeness:
    return a ^ b ? c : a
<!--more-->

2. Overloading is compile-time static binding and Overriding is run-time dynamic binding
------

In junior Java developer interviews, this is a popular question, the question would be:

{% codeblock lang:java %}
class Base{

}

class Derived extends Base{

}

class Test{
    public void methodA(Base b){
       System.out.println("Test.methodA(Base)");
    }
    public void methodA(Derived b){
        System.out.println("Test.methodA(Derived)");
    }
  
    public static void main(String []args){
        Test t = new Test();
        Base b = new Base();
        Base d = new Derived();
  
        t.methodA(b);
        t.methodA(d);
    }
}
{% endcodeblock %}

**What is the output?**

If your answer is

    Test.methodA(Base)
    Test.methodA(Derived)

This is wrong. For your surprise the actual output is

    Test.methodA(Base)
    Test.methodA(Base)

This is because the overloading is compile-time binding. When the compiler trying to figure out which `methodA` it is in `t.methodA(d)`, as far as the compiler knows is the definition of `d` is `Base`.

So, must be careful when overriding `Object.equals(otherObject)` function, override like this: `public boolean equals(Object other) {...}`


3. Java Object life cycle
------

1. Created
2. In use (strongly reachable)
3. Invisible
4. Unreachable
5. Collected
6. Finalized
7. Deallocated

4. How to declare i and j to make it be an infinite loop
------

{% codeblock lang:java %}
while( i <= j && i >= j && i != j){}
{% endcodeblock %}

This question also comes from [StackOverflow](http://stackoverflow.com/questions/8015146/how-to-declare-i-and-j-to-make-it-be-an-infinite-loop).

If `i` and `j` are primitive Java type, `i != j` means the int(or float, or whatever) value not equal, there will be no answer. However, `i != j` also means `i` and `j` are not the same Object. So, one of the answer is:

{% codeblock lang:java %}
Integer i=new Integer(1000);
Integer j=new Integer(1000);

System.out.println((i<=j)+" "+(i>=j)+" "+(i!=j)); 
{% endcodeblock %}

5. Invoke a java method when given the method name as a string
------

This question is very easy for scripting languages like Python and Perl. But for strong-type language like Java and C# we need a powerful tool called **reflector**.


>
Coding from the hip, it would be something like:

{% codeblock lang:java %}
java.lang.reflect.Method method;
try{  
    method = obj.getClass().getMethod(methodName, param1.class, param2.class,..);
} catch (SecurityException e){  
    // ...
} catch (NoSuchMethodException e){  
    // ...
}
{% endcodeblock %}

The parameters identify the very specific method you need (if there are several overloaded available, if the method has no arguments, only give methodName).
Then you invoke that method by calling

{% codeblock lang:java %}
try{  
    method.invoke(obj, arg1, arg2,...);
} catch(IllegalArgumentException e){

} catch(IllegalAccessException e){

} catch(InvocationTargetException e){    
    
}
{% endcodeblock %}

Again, leave out the arguments in .invoke, if you don't have any. But yeah. Read about [Java Reflection](http://java.sun.com/docs/books/tutorial/reflect/index.html).


BTW, solution above is from [StackOverflow](http://stackoverflow.com/questions/160970/how-do-i-invoke-a-java-method-when-given-the-method-name-as-a-string).


6. what is difference between string literal and new String("...")
------

The question is:
> What is difference between
{% codeblock lang:java %}
    String str =new String("abc");
{% endcodeblock %}
and
{% codeblock lang:java %}
    String str = "abc";
{% endcodeblock %}

The answer from [StackOverflow](http://stackoverflow.com/questions/3297867/difference-between-string-object-and-string-literal) is:

When you use a string literal the string can be [interned](http://en.wikipedia.org/wiki/String_interning) but when you use new String("...") you get a new string object.

In this example both string literals refer the same object:

{% codeblock lang:java %}
String a = "abc";
String b = "abc";
System.out.println(a == b);  // True
{% endcodeblock %}

Here two different objects are created and they have different references:

{% codeblock lang:java %}
String c = new String("abc");
String d = new String("abc");
System.out.println(c == d);  // False
{% endcodeblock %}

In general you should use the string literal notation when possible. It is easier to read and it gives the compiler a chance to optimize your code.

-------------

7. Memory usage of java collections
------

This article [From Java code to Java heap](http://www.ibm.com/developerworks/java/library/j-codetoheap/index.html) gives a comprehensive explanation of memory usage of popular java collection data structures.


