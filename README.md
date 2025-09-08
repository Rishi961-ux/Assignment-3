#include <iostream>
#include <stack>

class MinStack {
    std::stack<int> s;
    int minEle;

public:
    MinStack() {}

    void push(int x) {
        if (s.empty()) {
            s.push(x);
            minEle = x;
        } else if (x < minEle) {
            s.push(2 * x - minEle);
            minEle = x;
        } else {
            s.push(x);
        }
    }

    void pop() {
        if (s.empty()) return;

        int top = s.top();
        s.pop();

        if (top < minEle) {
            minEle = 2 * minEle - top;
        }
    }

    int top() {
        int top = s.top();
        if (top < minEle)
            return minEle;
        else
            return top;
    }

    int getMin() {
        return minEle;
    }

    bool empty() {
        return s.empty();
    }
};

int main() {
    MinStack ms;
    ms.push(3);
    ms.push(5);
    std::cout << ms.getMin() << "\n";
    ms.push(2);
    ms.push(1);
    std::cout << ms.getMin() << "\n";
    ms.pop();
    std::cout << ms.getMin() << "\n";
    ms.pop();
    std::cout << ms.top() << "\n";

    return 0;
}
