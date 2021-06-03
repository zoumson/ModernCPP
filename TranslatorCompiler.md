
# 1. Translator

## a. Definition
A translator accepts code expressed in source language S, and translates it to equivalent code expressed in another (target) language T.

## b. Examples:

* Compilers - translates high level code to low level code, e.g. Java -> JVM
* Assemblers - translates assembly language code to machine code, e.g. x86as -> x86
* High-level translators - translates code from one programming langage to another, e.g. Java -> C
* Decompilers - translates low-level code to high-level code, e.g. Java JVM bytecode -> Java

# 2. Interpreter

## a. Definition

* An S interpreter accepts code expressed in language S, and immediately executes that code. 
* It works by fetching, analysing, and executing one instruction at a time.

## b. Advantage

* Great when user is entering instructions interactively (think Python) and would like to get the output before putting in the next instruction. 
* Also useful when the program is to be executed only once. 
* or the program requires to be portable.

## c. Disadvantages

* Interpreting a program is much slower than executing native machine code
* Interpreting a high-level language is ~100 times slower
* Interpreting an intermediate-level (such as JVM bytecode) language is ~10 slower
* If an instruction is called repeatedly, it will be analysed repeatedly - time-consuming!

# 3. Differences

## a. Behaviour

* A compiler translates source code to machine code, but does not execute the source or object code.

* An interpreter executes source code one instruction at a time, but does not translate the source code.

## b. Performance

* A compiler takes quite a long time to translate the source program to native machine code, but subsequent execution is fast
* An interpreter starts executing the source program immediately, but execution is slow

# 4. Interpretive compilers

## a. Definition

An interpretive compiler is a good compromise between compilers and interpreters. It translates source program into virtual machine code, which is then interpreted.

## b. Behaviour

An interpretive compiler combines fast translation with moderately fast execution, provided that:

* VM code is lower than the source language, but higher than native machine code
* VM instructions have simple formats (can be quickly analysed by an interpreter)

## c. Example

JDK provides an interpretive compiler for Java.

# 5. Compile Time

## a. Reference

"A program written in a high-level language is called a source program or source code. Because a computer cannot execute a source program, a source program must be translated into machine code for execution. The translation can be done using another programming tool called an interpreter or a compiler." (Daniel Liang, "Introduction to JAVA programming", p8)

## b. Defintion

When we punch in high-level/human-readable code this is, at first, useless! It must be translated into a sequence of 'electronic happenings' in your tiny little CPU! The first step towards this is compilation. 

## c. Example of Compile time errors

* A Syntax Error - how can your code be compiled into machine level instructions if they are ambiguous??
* Your code needs to conform 100% to the syntactical rules of the language otherwise it cannot be compiled into working machine code.

# 6. Run Time

## a. Reference

"A compiler translates the entire source code into a machine-code file, and the machine-code file is then executed"

b. Example of run time error

* Running out of memory, a call to a recursive function for example might lead to stack overflow given a variable of a particular degree! How can this be anticipated by the compiler!? it cannot.

* Division by zero

# 7. Illustration

## a. High Level Source code to Machine code

The  source code is like the blueprint of a ship. It defines how the ship should be made.

If you hand off your blueprint to the shipyard, and they find a defect while building the ship, they'll stop building and report it to you immediately, before the ship has ever left the drydock or touched water. This is a compile-time error. The ship was never even actually floating or using its engines. The error was found because it prevented the ship even being made.

## b. Machine code running on a machine(Operating system)

When your code compiles, it's like the ship being completed. Built and ready to go. When you execute your code, that's like launching the ship on a voyage. The passengers are boarded, the engines are running and the hull is on the water, so this is runtime. If your ship has a fatal flaw that sinks it on its maiden voyage (or maybe some voyage after for extra headaches) then it suffered a runtime error.

# 8. const 

## a. Variable

* all type of variable
* Variable value is fixed.
* Evaluated either at run time or compile time
* Example: 
```
const int i = 10;// 10 is rvalue, used only once and its value is stolen and given to i
int x = 10;
const int y = x;// declared and initialized can't be changed later
y = = 2; //Error
```
## b. function

* Only member functions, function defined inside a given class
* The object called by these functions cannot be modified. 
* It is recommended to use const keyword so that accidental changes to object are avoided.
* A const member function can be called by any type of object. 
* Non-const functions can be called by non-const objects only.
* Exection time: compile time or run time
* Example:
```
class Person
{
	private:
	char  name[10];
	int age;

	public:
	Person():name("zouma"), age(20){}
	char * getName()const {return name;}
	int getAge() {return age;}
}

const Person p;
Person q;
p.getName();//ok
q.getName();//ok
p.getAge();//ok
q.getAge();//error
```

# 9. constexp

## a. Variable
* Any variable
* Declared, assigned and evaluated at compile time
* Act as preprocessor Macros
* Value can be used as c char string size
* Example:
```
constexp int a = 10; 10 is rvalue
const int b = 5;// 5 is rvalue
int c = 20;// 20 is rvalue
int d = c;// c is lvalue, has an address on the stack
constexp int e = a;//ok
constexp int f = b;//ok
constexp int g = c;//no
constexp int h = d;//no
char myStr[f] = "Adam";//ok
char str[c] ="Zouma";//no, c need to be constexp
```
## b. Function
* Any function, doesn't need to be necessarly member function
* Must have a single body return
* Arguments: constexp leads to constexp return type, else no error but result is not constexp type
* if argument is constexp, execution takes place at compile time
* if argument is not constexp, it becomes normal function, exectution takes place at run time
* Example:
```
constexp char* myName(char *name){return "zouma";}// ok
constexp int myAge(int age){// no
if(age > 10) return age;
else return 0;
}

constexp int myRealAge(int age){return age > 10 ? age : 0;}// ok

constexp char* me = myName("adam");// me is constexp, zouma is rvalue
char name[10] ="You";
constexp char* you = myName(name);// error, argument is not a constexp
const char* you1 = myName(name);//ok
char* you2 = myName(name);//ok
```


