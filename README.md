#include <iostream>
#include <stack>
#include <sstream>
#include <string>

using namespace std;

// Function to perform arithmetic operations
int performOperation(int operand1, int operand2, char op) {
    switch(op) {
        case '+': return operand1 + operand2;
        case '-': return operand1 - operand2;
        case '*': return operand1 * operand2;
        case '/': 
            if (operand2 == 0) {
                cerr << "Error: Division by zero!" << endl;
                exit(EXIT_FAILURE);
            }
            return operand1 / operand2;
        default:
            cerr << "Error: Unsupported operator '" << op << "'" << endl;
            exit(EXIT_FAILURE);
    }
}

// Function to evaluate postfix expression with multi-digit numbers and spaces
int evaluatePostfix(const string &expr) {
    stack<int> s;
    stringstream ss(expr);
    string token;

    while (ss >> token) {
        // Check if token is an operator or operand
        if (token.size() == 1 && (token[0] == '+' || token[0] == '-' || token[0] == '*' || token[0] == '/')) {
            if (s.size() < 2) {
                cerr << "Error: Invalid postfix expression" << endl;
                exit(EXIT_FAILURE);
            }
            int operand2 = s.top(); s.pop();
            int operand1 = s.top(); s.pop();

            int result = performOperation(operand1, operand2, token[0]);
            s.push(result);
        } else {
            // Assume token is an operand (number)
            try {
                int num = stoi(token);
                s.push(num);
            } catch (...) {
                cerr << "Error: Invalid token '" << token << "'" << endl;
                exit(EXIT_FAILURE);
            }
        }
    }

    if (s.size() != 1) {
        cerr << "Error: Invalid postfix expression" << endl;
        exit(EXIT_FAILURE);
    }

    return s.top();
}

int main() {
    string postfixExpr;

    cout << "Enter postfix expression (tokens separated by spaces): ";
    getline(cin, postfixExpr);

    int result = evaluatePostfix(postfixExpr);
    cout << "Result: " << result << endl;

    return 0;
}
