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









