---
title: Home
layout: home
---

# Welcome to my site!

This is a work in progress, stay tuned for more :sunglasses:

For now, enjoy this C++ code snippet... bonus points if you know what this could be used for.

```c++
#include <iostream>
#include <stdio.h>
#include <stdlib.h>

using namespace std;

class IntLinkedListNode {
  private:
    int data;
    IntLinkedListNode * next;

  public:
    IntLinkedListNode() {
      data = 0;
      next = NULL;
    }

    IntLinkedListNode(int value, IntLinkedListNode * node) {
      data = value;
      next = node;
    }

    int getData() {
      return data;
    }

    void setData(int value) {
      data = value;
    }

    IntLinkedListNode * getNext() {
      return next;
    }

    void setNext(IntLinkedListNode * node) {
      next = node;
    }
};

class IntLinkedList {
  private:
    IntLinkedListNode * front;
    IntLinkedListNode * back;

  public:
    IntLinkedList() {
      front = NULL;
      back = NULL;
    }

    IntLinkedListNode * getFront() {
      return front;
    }

    void setFront(IntLinkedListNode * node) {
      front = node;
    }

    IntLinkedListNode * getBack() {
      return back;
    }

    void setBack(IntLinkedListNode * node) {
      back = node;
    }
};

class IntStack {
  private:
    IntLinkedList stack;
    int size;

  public:
    IntStack(): stack() {
      size = 0;
    }

    void push(int value) {
      IntLinkedListNode * node = new IntLinkedListNode();
      node -> setData(value);
      node -> setNext(stack.getFront());
      stack.setFront(node);
      size++;
    }

    void pop() {
      IntLinkedListNode * front = stack.getFront();
      int value = front -> getData();

      if (size > 1) {
        stack.setFront(front -> getNext());
      }

      size--;
    }

    int peek() {
      if (size == 0) {
        return -1;
      }

      return stack.getFront() -> getData();
    }

    int getSize() {
      return size;
    }
};

int main() {
  IntStack stack;
  bool done = false;

  while (!done) {
    // Get user input
    char input;
    cout << "Please enter an operation (0-9, +, *, or =): ";
    cin >> input;

    if ('0' <= input && input <= '9') {
      // If 0-9, push the number onto the stack
      int value = input - '0'; // Convert char to integer
      stack.push(value);
    } else if (input == '+') {
      // If plus, pop top two numbers, add them, and push the result onto the stack
      if (stack.getSize() >= 2) {
        int a = stack.peek();
        stack.pop();
        int b = stack.peek();
        stack.pop();
        stack.push(a + b);
      } else {
        cout << "Invalid Operation: Not enough values in the stack" << endl;
      }
    } else if (input == '*') {
      // If star, pop top two numbers, multiply them, and push the result into the stack
      if (stack.getSize() >= 2) {
        int a = stack.peek();
        stack.pop();
        int b = stack.peek();
        stack.pop();
        stack.push(a * b);
      } else {
        cout << "Invalid Operation: Not enough values in the stack" << endl;
      }
    } else if (input == '=') {
      // If equals, print the number at the top of the stack
      int size = stack.getSize();

      if (size == 1) {
        int result = stack.peek();
        stack.pop();
        done = true;
        cout << "Result: " << result << endl;
      } else if (size > 1) {
        cout << "Invalid Operation: Too many values in the stack" << endl;
      } else {
        cout << "Invalid Operation: Not enough values in the stack" << endl;
      }
    } else {
      cout << "Invalid Input!" << endl;
    }
  }

  return 0;
}
```
