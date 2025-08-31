#include <iostream>
using namespace std;

#define MAX_SIZE 5

class Stack {
    int arr[MAX_SIZE];
    int top;
    
public:
    Stack() { top = -1; }
    bool isEmpty() {
        return top == -1;
    }
     bool isFull() {
        return top == MAX_SIZE - 1;
    }
     void push(int element) {
        if (isFull()) {
            cout << "Stack Overflow! Cannot push element.\n";
        } else {
            arr[++top] = element;
            cout << "" << element << " pushed onto the stack.\n";
        }
    }
      void pop() {
        if (isEmpty()) {
            cout << "Stack Underflow! Stack is empty.\n";
        } else {
            int popped = arr[top--];
            cout << "" << popped << " popped from the stack.\n";
        }
    }
     void peek() {
        if (isEmpty()) {
            cout << "Stack is empty. Nothing to peek.\n";
        } else {
            cout << "Top element is: " << arr[top] << "\n";
        }
    }
      void display() {
        if (isEmpty()) {
            cout << "Stack is empty.\n";
        } else {
            cout << "Stack contents (top to bottom):\n";
            for (int i = top; i >= 0; i--) {
                cout << "| " << arr[i] << " |\n";
            }
            cout << "-----\n";
        }
    }
};

int main() {
    Stack stack;
    int choice, element;

    while (true) {
        cout << "\n======= Stack Operations Menu =======\n";
        cout << "1. Push\n";
        cout << "2. Pop\n";
        cout << "3. Peek\n";
        cout << "4. Check if Empty\n";
        cout << "5. Check if Full\n";
        cout << "6. Display Stack\n";
        cout << "7. Exit\n";
        cout << "Enter your choice (1-7): ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter element to push: ";
                cin >> element;
                stack.push(element);
                break;
            case 2:
                stack.pop();
                break;
            case 3:
                stack.peek();
                break;
            case 4:
                if (stack.isEmpty())
                    cout << "Stack is empty.\n";
                else
                    cout << "Stack is not empty.\n";
                break;
            case 5:
                if (stack.isFull())
                    cout << "Stack is full.\n";
                else
                    cout << "Stack is not full.\n";
                break;
            case 6:
                stack.display();
                break;
            case 7:
                cout << "Exiting program. Goodbye!\n";
                return 0;
            default:
                cout << "Invalid choice. Please enter a number between 1 and 7.\n";
        }
    }
}
