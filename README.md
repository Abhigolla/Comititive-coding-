//Write a program for implementing A MINSTACK Which should support operations like PUSH,POP,OVERFLOW,UNDERFLOW & DISPLAY.
#include <stdio.h>
#include <stdlib.h>
#define MAX 5
struct MinStack {
    int stack[MAX];        
    int min_stack[MAX];  
    int top;               
};
void initstack(struct MinStack* minstack) {
    minstack->top = -1;
}
int isFull(struct MinStack* minstack) {
    return minstack->top == MAX - 1;
}
int isEmpty(struct MinStack* minstack) {
    return minstack->top == -1;
}
void push(struct MinStack* minstack, int value) {
    if (isFull(minstack)) {
        printf("Overflow: stack is full, cannot push element\n");
        return;
    }
    minstack->stack[++(minstack->top)] = value;
    if (minstack->top == 0) {
        minstack->min_stack[minstack->top] = value;
    } else {
        int currentMin = minstack->min_stack[minstack->top - 1];
        minstack->min_stack[minstack->top] = (value < currentMin) ? value : currentMin;
    }
}
int pop(struct MinStack* minstack) {
    if (isEmpty(minstack)) {
        printf("Underflow: stack is empty, cannot pop element\n");
        return -1;
    }
    return minstack->stack[minstack->top--];
}
int top(struct MinStack* minstack) {
    if (isEmpty(minstack)) {
        printf("Underflow: stack is empty, no top element\n");
        return -1;
    }
    return minstack->stack[minstack->top];
}
int getMin(struct MinStack* minstack) {
    if (isEmpty(minstack)) {
        printf("Underflow: stack is empty, no minimum element\n");
        return -1;
    }
    return minstack->min_stack[minstack->top];
}
void display(struct MinStack* minstack) {
    if (isEmpty(minstack)) {
        printf("Stack is empty\n");
        return;
    }

    printf("Stack elements: ");
    for (int i = 0; i <= minstack->top; i++) {
        printf("%d ", minstack->stack[i]);
    }
    printf("\nMinimum element so far: %d\n", getMin(minstack));
}
int main() {
    struct MinStack minstack;
    initstack(&minstack);
    push(&minstack, 10);
    push(&minstack, 20);
    push(&minstack, 5);
    push(&minstack, 30);
    display(&minstack);
    printf("Popped: %d\n", pop(&minstack));
    display(&minstack);
    printf("Top element: %d\n", top(&minstack));

    printf("Minimum element: %d\n", getMin(&minstack));
    pop(&minstack);
    pop(&minstack);
    pop(&minstack);
    pop(&minstack);  

    return 0;
}
