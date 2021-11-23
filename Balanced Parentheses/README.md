Valid Parentheses
----------
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

    Open brackets must be closed by the same type of brackets.
    Open brackets must be closed in the correct order.

 

Example 1:
--------
Input: s = "()"
Output: true

Example 2:
----------
Input: s = "()[]{}"
Output: true

Example 3:
----------
Input: s = "(]"
Output: false

Example 4:
----------
Input: s = "([)]"
Output: false

Example 5:
-----------
Input: s = "{[]}"
Output: true

 

Constraints:
-----------
    1 <= s.length <= 104
    s consists of parentheses only '()[]{}'.
Code:
----

#include<bits/stdc++.h>

using namespace std;


string isBalanced(string s)

{

    stack<char> st;
    int i;
    for(i = 0; i<s.length(); i++)
    {
        if(s[i] == '(' || s[i] == '[' || s[i] == '{')
        {
            st.push(s[i]);
        }
        else if(!st.empty())
        {
        if((s[i] == ')' && st.top() != '(') || (s[i] == ']' && st.top() != '[') || (s[i] == '}' && st.top() != '{'))
        {
            return "False";
        }
        else
        {
            st.pop();
        }
        }
        else{
            st.push(s[i]);
        }
    }
    if(st.empty())
    {
        return "True";
    }
    return "False";

}

int main()

{

    int t;
    cin>>t;
    string str;
    while(t--)
    {
        cin>>str;
        cout<<isBalanced(str)<<"\n";
    }
    return 0;
}
