#include <iostream>
#include <stack>
#include <string>
using namespace std;

int precedence(char op) {
    if(op == '+' || op == '-') 
        return 1;
    if(op == '*' || op == '/') 
        return 2;
    return 0;
}

bool isOperator(char ch) {
    return ch == '+' || ch == '-' || ch == '*' || ch == '/';
}

string infixToPostfix(const string& infix) {
    stack<char> s;
    string postfix;
    for(char ch : infix) {
        if (isspace(ch)) continue;
        if (isalnum(ch)) {
            postfix += ch;
        } 
        else if (ch == '(') {
            s.push(ch);
        } 
        else if (ch == ')') {
            while (!s.empty() && s.top() != '(') {
                postfix += s.top();
                s.pop();
            }
            if (!s.empty()) s.pop();  // pop '('
        } 
        else if (isOperator(ch)) {
            while (!s.empty() && precedence(s.top()) >= pre
