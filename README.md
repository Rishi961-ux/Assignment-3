#include <iostream>
#include <stack>
using namespace std;

int main() {
    string input = "DataStructure";
    stack<char> s;
    for (char ch : input) {
        s.push(ch);
    }
    string reversed = "";
    while (!s.empty()) {
        reversed += s.top();
        s.pop();
    }
    cout << reversed << endl;
    return 0;
}
