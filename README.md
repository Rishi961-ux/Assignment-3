#include <iostream>
#include <vector>
#include <stack>

std::vector<int> nearestSmallerToLeft(const std::vector<int>& A) {
    std::stack<int> s;
    std::vector<int> result;

    for (int x : A) {
        while (!s.empty() && s.top() >= x) {
            s.pop();
        }
        if (s.empty()) {
            result.push_back(-1);
        } else {
            result.push_back(s.top());
        }
        s.push(x);
    }

    return result;
}

int main() {
    std::vector<int> A = {4, 5, 2, 10, 8};
    std::vector<int> res = nearestSmallerToLeft(A);

    for (int x : res) {
        std::cout << x << " ";
    }

    return 0;
}
