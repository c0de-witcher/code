# code
#include<iostream>
#include<string>
using namespace std;

bool isRelationaloperator(string &str){
    return str=="<"||str==">"||str=="<="||str==">="||str=="!="||str=="==";
}

int main(){
    string input;
    cout<<"Enter the expression\n";
    getline(cin,input);
    string word1="";
    
    for(int i =0;i<input.size();i++){
        string word="";
        if(i+1<input.size()-1){
            word = input.substr(i,2);
            if(isRelationaloperator(word)){
                cout<<word<<" : relational  operator\n";
                i++;
                continue;
            }
        }
        
        word = input.substr(i,1);
        if(isRelationaloperator(word)){
            cout<<word<<" : relational operator";
        }
       
    }
    return 0;
}







#include<iostream>
#include<string>
using namespace std;

bool isConstant(string &word){
    if(word.empty())
    return false;
    
    int dotCount=0;
    
    int n = word.size();
    for(int i=0;i<n;i++){
       char ch = word[i];
       if(ch=='.'){
           dotCount++;
           if(dotCount==2)
           return false;
       }
       else if(!isdigit(ch))
       return false;
    }
    
    return true;
    
}

int main(){
    string input;
    cout<<"Enter the expression\n";
    getline(cin,input);
    string word="";
    
    for(int i =0;i<input.size();i++){
        char ch=input[i];
        if(isalnum(ch)|| ch=='.'){
            word+=ch;
        }
        else{
            if(!word.empty()){
                if(isConstant(word))
                {
                    cout<<word<<" : constant\n";
                   
                }
            }
             word="";
        }
    }
    return 0;
}






#include<iostream>
#include<string>
#include<vector>
#include<cctype>
#include<unordered_set>
using namespace std;

unordered_set<string> keyword {"if","else","while","for","int","float","char","return","main","double","bool"};

bool isKeyword(string &str){
    return keyword.find(str)!= keyword.end();
}

bool isOperator(char ch){
    return ch=='*'|| ch=='-'||ch=='+'||ch=='!'||ch=='/'||ch=='<'||ch=='>'||ch=='=';
}

int main(){
    string input;
    cout<<"enter the  symbol\n";
    getline(cin,input);
    string word="";
    int n= input.size();
    
    for(int i=0;i<n;i++){
        char ch=input[i];
        
        if(isOperator(ch)){
            if(!word.empty()){
                if(isKeyword(word))
                cout<<word<<" : Keyword\n";
                else
                cout<<word<<" : identifier\n";
                word = "";
            }
        }
        
        else if(ch==' '||ch==';'||ch=='('||ch==')'||ch=='{'||ch=='}'){
            if(!word.empty()){
                if(isKeyword(word))
                cout<<word<<" : keyword\n";
                else if(isdigit(word[0]))
                cout<<word<<" : number\n";
                else
                cout<<word<<" : identifier\n";
                word = "";
            }
            if(ch!=' '){
                cout<<ch<<" : symbol\n";
            }
        }
        
        else{
            word = word+ch;
        }
        
       
        
    }
    
     if(!word.empty()){
            if(isKeyword(word))
            cout<<word<<" : keyword\n";
            else if(isdigit(word[0]))
            cout<<word<<" : number\n";
            else
            cout<<word<<" : identifier\n";
        }
    return 0 ;
}










#include <iostream>
using namespace std;

#define MAX 100

class Stack {
private:
    int arr[MAX];
    int top;

public:
    Stack() {
        top = -1;
    }

    void push(int value) {
        if (top >= MAX - 1) {
            cout << "Stack Overflow!" << endl;
        } else {
            arr[++top] = value;
            cout << value << " pushed to stack." << endl;
        }
    }

    void pop() {
        if (top < 0) {
            cout << "Stack Underflow!" << endl;
        } else {
            cout << arr[top--] << " popped from stack." << endl;
        }
    }

    void peek() {
        if (top < 0) {
            cout << "Stack is empty." << endl;
        } else {
            cout << "Top element is: " << arr[top] << endl;
        }
    }

    void display() {
        if (top < 0) {
            cout << "Stack is empty." << endl;
        } else {
            cout << "Stack (top to bottom): ";
            for (int i = top; i >= 0; i--) {
                cout << arr[i] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Stack s;
    int choice, value;

    do {
        cout << "\n--- Stack Menu ---\n";
        cout << "1. Push\n2. Pop\n3. Peek\n4. Display\n5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter value to push: ";
            cin >> value;
            s.push(value);
            break;
        case 2:
            s.pop();
            break;
        case 3:
            s.peek();
            break;
        case 4:
            s.display();
            break;
        case 5:
            cout << "Exiting program.\n";
            break;
        default:
            cout << "Invalid choice! Try again.\n";
        }
    } while (choice != 5);

    return 0;
}
















#include <iostream>
#include <stack>
#include <vector>
#include <string>
using namespace std;

// Function to check if top of stack matches RHS of any production
bool reduce(stack<string>& st) {
    // Reduce id to E
    if (!st.empty() && st.top() == "id") {
        st.pop();
        st.push("E");
        cout << "Reduce: E → id" << endl;
        return true;
    }

    // Reduce E + E to E
    if (st.size() >= 3) {
        string top1 = st.top(); st.pop();
        string top2 = st.top(); st.pop();
        string top3 = st.top(); st.pop();

        if (top1 == "E" && top2 == "+" && top3 == "E") {
            st.push("E");
            cout << "Reduce: E → E + E" << endl;
            return true;
        } else {
            // Restore if no match
            st.push(top3);
            st.push(top2);
            st.push(top1);
        }
    }

    // Reduce E * E to E
    if (st.size() >= 3) {
        string top1 = st.top(); st.pop();
        string top2 = st.top(); st.pop();
        string top3 = st.top(); st.pop();

        if (top1 == "E" && top2 == "*" && top3 == "E") {
            st.push("E");
            cout << "Reduce: E → E * E" << endl;
            return true;
        } else {
            st.push(top3);
            st.push(top2);
            st.push(top1);
        }
    }

    return false;
}

int main() {
    string input;
    cout << "Enter expression with space (e.g., id + id * id): ";
    getline(cin, input);

    // Tokenize the input by space
    vector<string> tokens;
    string token;
    for (char c : input) {
        if (c == ' ') {
            if (!token.empty()) {
                tokens.push_back(token);
                token.clear();
            }
        } else {
            token += c;
        }
    }
    if (!token.empty()) tokens.push_back(token);

    stack<string> st;
    int i = 0;

    cout << "\n--- Parsing Steps ---\n";

    while (i < tokens.size()) {
        // Shift
        st.push(tokens[i]);
        cout << "Shift: " << tokens[i] << endl;
        i++;

        // Try reducing as much as possible after each shift
        while (reduce(st));
    }

    // Final reduction
    while (reduce(st));

    if (st.size() == 1 && st.top() == "E") {
        cout << "\nParsing successful: Input accepted." << endl;
    } else {
        cout << "\nParsing failed: Input not accepted." << endl;
    }

    return 0;
}












#include <iostream>
#include <stack>
#include <vector>
#include <string>
using namespace std;

// Function to check if a character is an operator
bool isOperator(char op) {
    return op == '+' || op == '-' || op == '*' || op == '/';
}

// Function to get precedence of operator
int precedence(char op) {
    if (op == '*' || op == '/') return 2;
    if (op == '+' || op == '-') return 1;
    return 0;
}

// Convert infix to postfix using Shunting Yard Algorithm
vector<string> infixToPostfix(string expr) {
    vector<string> postfix;
    stack<char> opStack;
    string operand = "";

    for (char ch : expr) {
        if (ch == ' ') continue;

        if (isalnum(ch)) {
            operand += ch;
        } else {
            if (!operand.empty()) {
                postfix.push_back(operand);
                operand = "";
            }

            if (isOperator(ch)) {
                while (!opStack.empty() && precedence(opStack.top()) >= precedence(ch)) {
                    postfix.push_back(string(1, opStack.top()));
                    opStack.pop();
                }
                opStack.push(ch);
            }
        }
    }

    if (!operand.empty()) {
        postfix.push_back(operand);
    }

    while (!opStack.empty()) {
        postfix.push_back(string(1, opStack.top()));
        opStack.pop();
    }

    return postfix;
}

// Generate Three Address Code from postfix
void generateTAC(vector<string> postfix, string lhs) {
    stack<string> st;
    int tempCount = 1;

    for (string token : postfix) {
        if (token == "+" || token == "-" || token == "*" || token == "/") {
            string op2 = st.top(); st.pop();
            string op1 = st.top(); st.pop();
            string temp = "t" + to_string(tempCount++);
            cout << temp << " = " << op1 << " " << token << " " << op2 << endl;
            st.push(temp);
        } else {
            st.push(token);
        }
    }

    // Final assignment
    cout << lhs << " = " << st.top() << endl;
}

int main() {
    string expr;
    cout << "Enter expression (e.g., a = b + c * d): ";
    getline(cin, expr);

    // Separate LHS and RHS
    size_t eq = expr.find('=');
    if (eq == string::npos) {
        cout << "Invalid expression!" << endl;
        return 1;
    }

    string lhs = expr.substr(0, eq);
    string rhs = expr.substr(eq + 1);

    // Trim spaces
    lhs.erase(remove(lhs.begin(), lhs.end(), ' '), lhs.end());
    rhs.erase(remove(rhs.begin(), rhs.end(), ' '), rhs.end());

    // Generate TAC
    vector<string> postfix = infixToPostfix(rhs);
    cout << "\nThree Address Code:\n";
    generateTAC(postfix, lhs);

    return 0;
}











