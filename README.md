# Brief Review (cont.)
## C++ (cont.)
* <img width="410" alt="Screen Shot 2022-06-07 at 4 32 17 PM" src="https://user-images.githubusercontent.com/89602311/172486439-ea5cb694-f343-483e-889d-c5eb02fa4843.png">
* <img width="568" alt="Screen Shot 2022-06-07 at 4 36 21 PM" src="https://user-images.githubusercontent.com/89602311/172487042-4279687d-d19b-48d2-844d-da46556b5069.png">
```
#include <iostream>
using namespace std;
int func(int *p, int &r) // num1 is 2, num2 is 3
{
    *p -= 1; // num1 becomes 1
    r += 2; // num2 becomes 5
    return *p + r; // 1 + 5 
}
int func2(int *p1, int *p2) // num1 is 2, num2 is 3, p1 is pointing to 2 (num1)
{
    p1 = p2; // p1 is pointing to num2 (3)
    *p1 += 2; // num2 is changed to 5
    return *p1 + *p2; // 5 + 5
}
int main()
{
    int num1 = 2, num2 = 3;
    cout << func2(&num1, num2) << endl; // 10
    cout << "num1 = " << num1 << endl; // 2
    cout << "num2 = " << num2 << endl; //5
    return 0;
} 
```
* <img width="617" alt="Screen Shot 2022-06-07 at 4 43 07 PM" src="https://user-images.githubusercontent.com/89602311/172487963-9e2f2ae6-2cc5-49b4-be3e-130309b60dbe.png">
* Create Makefile for your project
  - makefile wase your C++ project management
    - Pre-specify the targets and rules
    - Save time on typing and compilation
  - Learn the basic way to compile your code on our department server
    ```
    all: program
    program: clean main.o file1.o
             g++ ‐g main.o file1.o ‐o program
    main.o: main.cpp
            g++ -g -c main.cpp
    file1.o: file1.cpp file1.h
             g++ ‐g ‐c file1.cpp ‐o file1.o
    clean: 
           rm  ‐f *.o program
    ```
## Recursion
* Strongly linked to recursive definition
  - Recursive definition: generate the terms sequentially
    - E.g, Fibonacci sequence f0 = 0, f1 = 1, fn = fn-1 + fn-2 for n = 2,3,4
    - Understnad in a forward way (f1->f2->f3...->fn-1 ->fn)
  <img width="198" alt="Screen Shot 2022-06-07 at 5 26 37 PM" src="https://user-images.githubusercontent.com/89602311/172493493-447391dc-f147-465d-b742-c1267518c798.png">
* Recursive definition is illustrated in a forward way
* Recursion can be treated in the backward way
  - E.g., in Fibonacci sequence, to get 𝑓7 we need 𝑓6 and 𝑓5; then to get 𝑓6 we need 𝑓5 and 𝑓4, and to get 𝑓5 we need 𝑓4 and 𝑓3; so on so forth.
    - To get 𝑓3, 𝑓4, 𝑓5, 𝑓6 are the same problem as to get 𝑓7.
    - This means we are calling the same function, only the parameter will be changed
    - In this backward way, the size/scale/complexity of the problems/subproblems will be reduced, and at the end we will reach the base case(s) and produce a result for the entire problem (Break down the big problem into smaller ones)
* <img width="465" alt="Screen Shot 2022-06-07 at 5 31 49 PM" src="https://user-images.githubusercontent.com/89602311/172494080-d2635a8e-f2aa-4937-92bf-5297b8e7e066.png">
* How to design recursive algorithms?
  - The recursive definition can always be a good start
    - Find the solution based on previous subproblems
        - Have a try on some small cases from the base case(s)
        - How to divide the problem into similar smaller parts?
    - The key is to understand what’s a subproblem
        - Build the relation to link to the subproblems
        - This link is the recurrence relation (recursive step)
  - The correctness is based on the recursive step and the base case(s)
    - Just like the Domino effect:
      - Give a push at the beginning (base case)
      - Ensure the next domino will be knocked over (recursive step)
* Example: recursion algorithm for Fibonacci sequence
  - Recursive def.: f0 = 0, f1 = 1, and fn = fn-1 + fn-2 for n = 2,3,4,..
  - Recursive algo.: (1) pseudocode and (2) C++ code
  - (1) and (2)
  ```
  procedure fibonacci(n: nonnegative integer)
  if n = 0 then return 0
  else if n = 1 then return 1
  else return fibonacci(n - 1) + fibonacci(n - 2)
  {output is fibonacci(n)} 
  ```
  ``` 
  int fibonacci(int n){ //assume n is nonnegative
  if (n <= 1) return n;
  return fibonacci(n‐1) + fibonacci(n‐2);
  }
  ``` 
* The Hanoi Tower
  - A good example of solving a big problem using the divide and conquer and recursion technology
  - https://www.mathsisfun.com/games/towerofhanoi.html
  - <img width="492" alt="Screen Shot 2022-06-07 at 5 46 40 PM" src="https://user-images.githubusercontent.com/89602311/172495592-cd29a19a-5810-4d99-8a52-b0ff3c1ac2f2.png">
* Function design: move(disks, start, end, temp)
  - disks: number of disks
  - start: start position (1,2 or 3)
  - end: end position (1, 2 or 3)
  - temp: temporary storage position (1,2 or 3)
  - <img width="504" alt="Screen Shot 2022-06-07 at 6 02 14 PM" src="https://user-images.githubusercontent.com/89602311/172497205-f270a402-deec-4196-abcb-a562755c7f10.png">
```
// Recursive solution for Hanoi Tower
// Move 63 disks from tower 1 to 2 (tower 3 temporary).
main() {          
move(63, 1, 2, 3);
}
void move(int count, int start, int finish, int temp) {
  if (count > 0) {
    move(count ‐ 1, start, temp, finish);
    cout << "Move the top disk from " << start
         << " to " << finish << "." << endl;
    move(count ‐ 1, temp, finish, start);
  }
}
```
## Stack
* last-in--first-out(LIFO)
* <img width="218" alt="Screen Shot 2022-06-07 at 6 11 50 PM" src="https://user-images.githubusercontent.com/89602311/172498134-46538d86-91a3-4461-a98c-8eb8a54433b9.png">
``` 
template <typename Type>
class Stack {
  private:
    int stack_size;
    int array_capacity;
    Type *array;
  public:
   Stack( int n = 10 );
    ~Stack();
    bool isEmpty() const;
    void push( Type const & );
    Type pop();
};
```
## Queue
* first-in--first-out (FIFO)
* <img width="244" alt="Screen Shot 2022-06-07 at 6 14 54 PM" src="https://user-images.githubusercontent.com/89602311/172498430-ca3ebc5f-432a-4221-b2f8-cbda02c7ca64.png">
```
template <typename Type>
class Queue{
  private:
    int queue_size;
    int ifront;
    int iback;
    int array_capacity;
    Type *array;
  public:
    Queue( int n = 10 );L
    ~Queue();
    bool isEmpty() const;
    void enqueue(Type const &);
    Type dequeue();
};
```
## What's next
* The implementations could vary
  - Linked implementation in Programming II
  - Contiguous implementation as above
* There are generalized operations
  - E.g., push and pop for a stack
  - E.g., dequeue and enqueue for a queue
* Seperate implementation from specification
  - Abstract Data Types (ADT)
* Doing it is different from just reading it
  - Though the codes are given, still consider yourselves as the designer of the programs

