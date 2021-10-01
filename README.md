# DSA
Write DSA Codes into it
All codes will be accepted after checking! Do not Copy and Paste code
Infix to Postfix expression using stack
-------------------------//----CODE--------------//------------------------------------------->>>>>>>>>>>>>>>>>------------------>>
#include<bits/stdc++.h>
#include<stack>
using namespace std;


 // } Driver Code Ends


    int prec(char ch){
    if(ch == '^')
        return 3;
    else if (ch == '*' || ch == '/')
        return 2;
    else if(ch == '+' || ch == '-')
        return 1;
    else return -1;
   }
    //Function to convert an infix expression to a postfix expression.
    string infixToPostfix(string s)
    {
    stack<char> st;
    string result = "";
    char ch;
    for(int i = 0 ; i< s.length(); i++){
        ch = s[i];
        if((65 <= ch && ch <= 90) || (97<=ch && ch <= 122))
            result += ch;
        else if( ch == '('){
            st.push(ch);
        }
        else if(ch == ')'){
            while(!st.empty() && st.top() != '('){
                result += st.top();
                st.pop();
            }
            st.pop();
        }
        else{
            if(st.empty() || (prec(ch) > prec(st.top())) || ((prec(ch) == prec(st.top()) && prec(ch) == 3)) )
                st.push(ch);
            else{
                while(!st.empty() && prec(ch)<= prec(st.top())){
                    result += st.top();
                    st.pop();
                }
                st.push(ch);
            }
        }
    }
    while (!st.empty())
    {
        result += st.top();
        st.pop();
    }
    return result;
    }
};


int main()
{
    int t;
    cin>>t;
    cin.ignore(INT_MAX, '\n');
    while(t--)
    {
        string exp;
        cin>>exp;
        cout<<infixToPostfix(exp)<<endl;
    }
    return 0;
}
