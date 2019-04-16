# Interface, Abstract Class, Inheritance

语法层面

abstract class的方式定义Demo抽象类的方式如下：
```java
abstract class Demo ｛
    abstract void method1();
    abstract void method2();
    …
｝
```

interface的方式定义Demo抽象类的方式如下
```java
interface Demo {
    void method1();
    void method2();
    …
}
```
在abstract class方式中，Demo可以有自己的数据成员，也可以有非abstarct的成员方法，而在interface方式的实现中，Demo只能够有静态的不能被修改的数据成员（也就是必须是static final的，不过在interface中一般不定义数据成员），所有的成员方法都是abstract的。从某种意义上说，interface是一种特殊形式的abstract class。

abstract class表示的是"is a"关系，interface表示的是"like a"关系，大家在选择时可以作为一个依据，当然这是建立在对问题领域的理解上的

abstract class 是对本质的抽象，目的是代码重复利用。比如把男人女人抽象为人。所以一个class 只能有一个abstract class, 不能是男人又是女人。

Interface 是对动作行为的抽象，目的是约束动作。比如吃饭喝水走路，所以一个class 可以有多个interface. 一个interface 也可以有多个interface, 因为可以在走路里，走山路走马路。


# Inheritance: is the process by which one object acquires the properties of another object

Why multiple inheritance is not supported through class in Java, but it can be possible through interface ?

Multiple inheritance is not supported by class because of ambiguity. In case of interface there is no ambiguity because implementation to method(s) is provided by the implementing class. 


# 浅谈Java面试过程中的Encapsulation, Inheritance and Polymorphism

## Encapsulation: is the mechanism that binds together code and data it manipulates and keeps both safe from outside interference and misuse.

我们常说OOP 的coding要考虑到maintainability, flexibility and extensibility，换句话说， Encapsulation的好坏直接影响着code本身的质量。Open for extension, Closed for modification. 从下面的例子中我们可以发现Encapsulation的作用：

```java

public class EncapTest{
   private String name;
   private String idNum;
   private int age;
   public int getAge(){
      return age;
   }
   public String getName(){
      return name;
   }
   public String getIdNum(){
      return idNum;
   }
   public void setAge( int newAge){
      age = newAge;
   }
   public void setName(String newName){
      name = newName;
   }


   public void setIdNum( String newId){
      idNum = newId;
   }
}

```

在上述的例子里我们可以看出Class EncapTest有两个private的member, 分别是 name 和 idNum. 但是我们向外部提供了public的接口允许我们去做set跟get的action. 或许有人会问上述的例子中，getter跟setter其实跟直接获取attributes或者给attributes赋值没有任何区别，但是为什么我们还是需要提供getter或者setter呢？

其实上述的例子只是一个最为基本的概念，在实际应用中，如果我们将attributes变成public, 那么用户就可以随意的set其中的value, 这在工业上是一种相当危险的行为，因此大多数的setter内部都会调用相应的的validation作为检查，这样customer的input只有在通过检查，符合的规定之后才能后对里面的attribute进行赋值。当然，想getter和setter这种boiler plate的代码都可以自动生成，或者直接用attribute定义，比如Java的Lombok, etc.

Benefits of Encapsulation:

The fields of a class can be made read-only or write-only.
A class can have total control over what is stored in its fields.
The users of a class do not know how the class stores its data. A class can change the data type of a field and users of the class do not need to change any of their code.


## Inheritance: is the process by which one object acquires the properties of another object
有时候面试官会问面试者什么是 IS-A relationship? 其实IS-A relationship就指的是Inheritance。

```java

public class Animal{
}

public class Mammal extends Animal{
}

public class Reptile extends Animal{
}

public class Dog extends Mammal{
}

public class Dog extends Mammal{

   public static void main(String args[]){

      Animal a = new Animal();
      Mammal m = new Mammal();
      Dog d = new Dog();

      System.out.println(m instanceof Animal);
      System.out.println(d instanceof Mammal);
      System.out.println(d instanceof Animal);
   }
}

```

我们有一个基本类叫做Animal, 然后我们定义了如下IS-A relationship. Mammal 是一种 Animal, Reptile 是另外一种 Animal. Mammal跟Reptile是相互并行的关系，他们的共同点就是他们都是一种 Animal. 而最后的 Dog 被明确的指出就是一种 Mammal 同时，我们也能说Dog 是一种 Animal.

Now, if we consider the IS-A relationship, we can say:

Mammal IS-A Animal

Reptile IS-A Animal

Dog IS-A Mammal

Hence : Dog IS-A Animal as well 

因此上面的code will all print "true".



## Polymorphism: is the feature that allows one interface to be used for general class actions.
从字面上理解，多态就是一种类型表现出多种状态。多态在Java用有两种实现方式， 我们通常称为静态绑定跟动态绑定。静态绑定就是说在程序运行之前进行绑定，由编译器和连接程序实现。比如overloading。 动态绑定在运行时根据对象的类型进行绑定，由方法调用机制实现。比如overriding。如何理解多态，请看下面的例子：

```java

public class Employee
{
   private String name;
   private String address;
   private int number;
   public Employee(String name, String address, int number)
   {
      System.out.println("Constructing an Employee");
      this.name = name;
      this.address = address;
      this.number = number;
   }
   public void mailCheck()
   {
      System.out.println("Mailing a check to " + this.name
       + " " + this.address);
   }
   public String toString()
   {
      return name + " " + address + " " + number;
   }
   public String getName()
   {
      return name;
   }
   public String getAddress()
   {
      return address;
   }
   public void setAddress(String newAddress)
   {
      address = newAddress;
   }
   public int getNumber()
   {
     return number;
   }
}


/* File name : Salary.java */
public class Salary extends Employee
{
   private double salary; //Annual salary
   public Salary(String name, String address, int number, double
      salary)
   {
       super(name, address, number);
       setSalary(salary);
   }
   public void mailCheck()
   {
       System.out.println("Within mailCheck of Salary class ");
       System.out.println("Mailing check to " + getName()
       + " with salary " + salary);
   }
   public double getSalary()
   {
       return salary;
   }
   public void setSalary(double newSalary)
   {
       if(newSalary >= 0.0)
       {
          salary = newSalary;
       }
   }
   public double computePay()
   {
      System.out.println("Computing salary pay for " + getName());
      return salary/52;
   }
}
/* File name : VirtualDemo.java */
public class VirtualDemo
{
   public static void main(String [] args)
   {
      Salary s = new Salary("Mohd Mohtashim", "Ambehta, UP", 3, 3600.00);
      Employee e = new Salary("John Adams", "Boston, MA", 2, 2400.00);
      System.out.println("Call mailCheck using Salary reference --");
      s.mailCheck();
      System.out.println("\n Call mailCheck using Employee reference--");
      e.mailCheck();
    }
}

```

This would produce the following result:

Constructing an Employee

Constructing an Employee

Call mailCheck using Salary reference --

Within mailCheck of Salary class

Mailing check to Mohd Mohtashim with salary 3600.0

Call mailCheck using Employee reference--

Within mailCheck of Salary class - Mailing check to John Adams with salary 2400.0

