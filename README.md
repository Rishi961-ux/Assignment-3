#include <iostream>
#include <stack>
#include <string>

using namespace std;

// Function to return precedence of operators
int precedence(char op) {
    if (op == '*' || op == '/')
        return 2;
    if (op == '+' || op == '-')
        return 1;
    return 0;  // For '(' or others
}

// Helper function to check if character is an operand (letter or digit)
bool isOperand(char ch) {
    // Check if uppercase or lowercase letter OR digit
    return (ch >= 'A' && ch <= 'Z') ||
           (ch >= 'a' && ch <= 'z') ||
           (ch >= '0' && ch <= '9');
}

string infixToPostfix(const string& expression) {
    stack<char> stk;
    string output;

    // Traditional for loop with index
    for (size_t i = 0; i < expression.length(); ++i) {
        char ch = expression[i];

        if (isOperand(ch)) {
            // Operand: add to output
            output += ch;
            output += ' ';
        }
        else if (ch == '(') {
            stk.push(ch);
        }
        else if (ch == ')') {
            // Pop until '(' is found
            while (!stk.empty() && stk.top() != '(') {
                output += stk.top();
                output += ' ';
                stk.pop();
            }
            if (!stk.empty()) stk.pop();  // Remove '('
        }
        else {
            // Operator encountered
            while (!stk.empty() && precedence(stk.top()) >= precedence(ch)) {
                output += stk.top();
                output += ' ';
                stk.pop();
            }
            stk.push(ch);
        }
    }

    // Pop all remaining operators
    while (!stk.empty()) {
        output += stk.top();
        output += ' ';
        stk.pop();
    }

    // Remove trailing space if present
    if (!output.empty())
        output.pop_back();

    return output;
}

int main() {
    string expr = "A+B-C*(D+E)";
    cout << "Infix: " << expr << endl;
    cout << "Postfix: " << infixToPostfix(expr) << endl;
    return 0;
}
