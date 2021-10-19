# clear-code
//clear any code program from spaces and comments
#include <iostream>
#include<bits/stdc++.h>
#include<vector>
using namespace std;

string removeComments(string prgm)
{
    int n = prgm.length();
    string res;

// Flags to indicate that single line and multiple line comments
// have started or not.
    bool s_cmt = false;
    bool m_cmt = false;


// Traverse the given program
    for (int i=0; i<n; i++)
    {
// If single line comment flag is on, then check for end of it
        if (s_cmt == true && prgm[i] == '\n')
            s_cmt = false;

// If multiple line comment is on, then check for end of it
        else if  (m_cmt == true && prgm[i] == '*' && prgm[i+1] == '/')
            m_cmt = false,  i++;

// If this character is in a comment, ignore it
        else if (s_cmt || m_cmt)
            continue;

// Check for beginning of comments and set the approproate flags
        else if (prgm[i] == '/' && prgm[i+1] == '/')
            s_cmt = true, i++,res=res+"\n";
        else if (prgm[i] == '/' && prgm[i+1] == '*')
            m_cmt = true,  i++;

// If current character is a non-comment character, append it to res
        else  res += prgm[i];
    }
    return res;
}

int main()
{
    cin.tie(0);
    cin.sync_with_stdio(0);

    string str,s="";
    string m[52]= {""};
    while ( getline(cin, str))
    {
        s=s+str+"\n";
    }


    for(int i=0; i<s.size(); i++)
    {
        if(s[i] == ' ' && (s[i+1] == ' ' || s[i+1] == '\n'))
        {
            s.erase(i, 1);
            i--;
        }
    }



    s=removeComments(s);

    while(s.find("\n\n") != std::string::npos)
        s.erase(s.find("\n\n"), 1);

    for(int j = 0; j<s.size(); j++)
        if(s[j] == '\n' && j == 0) continue;
        else cout << s[j];

    return 0;
}
