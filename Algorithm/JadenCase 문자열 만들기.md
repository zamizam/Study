## 프로그래머스 Lv.2 JadenCase 문자열 만들기

생각이 짧았던걸까... 코드를 단순하게 구현할 생각을 못 했던걸까..ㅋㅋ;;

코테에서 여러가지 함수 구현해봤자 의미없다는걸 가져왔다 ^^

### 문제 설명
JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)

문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

### 제한 조건
- s는 길이 1 이상 200 이하인 문자열입니다.
- s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
  - 숫자는 단어의 첫 문자로만 나옵니다.
  - 숫자로만 이루어진 단어는 없습니다.
  - 공백문자가 연속해서 나올 수 있습니다.

### 입출력 예
| s | result |
|---|-----|
|"3people unFollowed me" |	"3people Unfollowed Me" |
|"for the last week" |	"For The Last Week" |

## 띄어쓰기 구분하기 케이스별 실패작
1. strtok (실패) [여기](#1차-strtok-도전)
2. stringstream (실패) [여기](#2차-stringstream-도전)
3. 문자로 먼저 전부 바꾸고 벡터 안 쓰고 stringstream (실패) [여기](#3차-소문자로-먼저-전부-바꾸고-벡터-안-쓰고-stringstream-도전)
4. 문자열별 냅다 비교 (성공) [여기](#4차-문자열끼리-그냥-비교-도전)



### 1차 strtok 도전
```
#include <string>
#include <vector>
#include <string.h>
#include <cctype>

using namespace std;

string solution(string s) {
    string answer = "";
    
    char sTemp[256] = {0, };
    strcpy(sTemp, s.c_str());
    char* pToken = strtok(sTemp, " ");
    
    vector<string> v;
    
    while( pToken != nullptr)
    {
        string a = string(pToken);
        if( a[0] >= 'a' && a[0] <= 'z')
        {
            a[0] = toupper(a[0]);
        }
        
        for(int i = 1; i < a.length(); i++ )
        {
            if( a[i] >= 'A' && a[i] <= 'Z')
            {
                a[i] = tolower(a[i]);
            }
        }
        v.push_back(a);
        pToken = strtok(nullptr, " ");
    }
    
    for(int i = 0; i < v.size(); i++)
    {
        answer += v[i];
        if( i == v.size()-1 )
            break;
        
        answer += " ";
    }
    
    return answer;
}
```

```테스트 1 〉	통과 (0.02ms, 4.2MB)
테스트 2 〉	실패 (0.01ms, 4.21MB)
테스트 3 〉	통과 (0.01ms, 4.2MB)
테스트 4 〉	실패 (0.02ms, 4.13MB)
테스트 5 〉	실패 (0.02ms, 3.69MB)
테스트 6 〉	통과 (0.02ms, 4.2MB)
테스트 7 〉	통과 (0.01ms, 4.21MB)
테스트 8 〉	실패 (0.01ms, 3.68MB)
테스트 9 〉	실패 (0.02ms, 4.14MB)  //응 실패...
테스트 10 〉	통과 (0.01ms, 4.52MB)
테스트 11 〉	실패 (0.02ms, 4.21MB)
테스트 12 〉	실패 (0.01ms, 3.63MB)
테스트 13 〉	실패 (0.02ms, 4.22MB)
테스트 14 〉	실패 (0.02ms, 3.63MB)
테스트 15 〉	통과 (0.02ms, 3.75MB)
테스트 16 〉	통과 (0.01ms, 4.2MB)
테스트 17 〉	실패 (0.01ms, 4.43MB)
테스트 18 〉	통과 (0.01ms, 4.21MB)
```
### 2차 stringstream 도전
```
#include <string>
#include <vector>
#include <sstream>
#include <cctype>

using namespace std;

string solution(string s) {
    
    string answer = "";
    
    istringstream input(s);
    vector<string> v;
    string buff = "";
    
    while( getline(input, buff, ' ') )
    {
        if( buff[0] >= 'a' && buff[0] <= 'z')
        {
            buff[0] = toupper(buff[0]);
        }
        
        for(int i = 1; i < buff.size(); i++ )
        {
            if( buff[i] >= 'A' && buff[i] <= 'Z')
            {
                buff[i] = tolower(buff[i]);
            }
        }
        
        v.push_back(buff);
    }
    
    for(int i = 0; i < v.size(); i++)
    {
        answer += v[i];
        if( i == v.size() - 1)
            break;
        
        answer += " ";
    }
    
    return answer;
}
```
```
테스트 1 〉	통과 (0.02ms, 3.75MB)
테스트 2 〉	통과 (0.03ms, 4.2MB)
테스트 3 〉	통과 (0.03ms, 4.15MB)
테스트 4 〉	통과 (0.04ms, 4.14MB)
테스트 5 〉	통과 (0.02ms, 4.14MB)
테스트 6 〉	통과 (0.02ms, 4.2MB)
테스트 7 〉	통과 (0.03ms, 4.15MB)
테스트 8 〉	실패 (0.02ms, 4.15MB) // 응.. 2차실패..
테스트 9 〉	통과 (0.02ms, 4.21MB)
테스트 10 〉	통과 (0.02ms, 3.63MB)
테스트 11 〉	통과 (0.03ms, 4.21MB)
테스트 12 〉	통과 (0.03ms, 3.67MB)
테스트 13 〉	통과 (0.02ms, 4.21MB)
테스트 14 〉	통과 (0.02ms, 4.02MB)
테스트 15 〉	통과 (0.02ms, 4.15MB)
테스트 16 〉	통과 (0.03ms, 4.21MB)
테스트 17 〉	통과 (0.02ms, 4.21MB)
테스트 18 〉	통과 (0.02ms, 4.14MB)
```
### 3차 소문자로 먼저 전부 바꾸고 벡터 안 쓰고 stringstream 도전
```
#include <string>
#include <vector>
#include <sstream>
#include <cctype>

using namespace std;

string solution(string s) {
    string answer = "";
    
    for( char& ch : s)
    {
        if( ch >= 'A' && ch <= 'Z')
        {
            ch |= 32;
        }
    }
    
    istringstream input(s);
    
    vector<string> v;
    string buff;
    
    int i = 0; 
    
    while( getline(input, buff, ' ') )
    {
        if( i != 0 )
        {
            answer += " ";
        }
        
        if( buff[0] >= 'a' && buff[0] <= 'z' )
        {
            buff[0] = toupper(buff[0]);
        }
        
        answer += buff;
        i++;
    }
   
    
    return answer;
}
```
```
테스트 1 〉	통과 (0.02ms, 4.4MB)
테스트 2 〉	통과 (0.02ms, 4.2MB)
테스트 3 〉	통과 (0.02ms, 4.14MB)
테스트 4 〉	통과 (0.02ms, 4.13MB)
테스트 5 〉	통과 (0.02ms, 4.22MB)
테스트 6 〉	통과 (0.02ms, 4.12MB)
테스트 7 〉	통과 (0.03ms, 4.21MB)
테스트 8 〉	실패 (0.02ms, 3.7MB)    // 메모리는 줄였으나 3차 실패...!!
테스트 9 〉	통과 (0.02ms, 4.21MB)
테스트 10 〉	통과 (0.02ms, 4.22MB)
테스트 11 〉	통과 (0.02ms, 4.16MB)
테스트 12 〉	통과 (0.02ms, 4.15MB)
테스트 13 〉	통과 (0.02ms, 4.14MB)
테스트 14 〉	통과 (0.02ms, 4.17MB)
테스트 15 〉	통과 (0.02ms, 4.15MB)
테스트 16 〉	통과 (0.03ms, 4.21MB)
테스트 17 〉	통과 (0.02ms, 3.68MB)
테스트 18 〉	통과 (0.02ms, 4.21MB)
```
### 4차 문자열끼리 그냥 비교 도전
```
#include <string>
#include <vector>
#include <sstream>
#include <cctype>

using namespace std;

string solution(string s) {
    string answer = "";

    //전부 소문자로
    for( char& ch : s )
    {
        ch |= 32;
    }

    for( int i = 0; i < s.size(); i++ )
    {
        //첫문장이 소문자면
        if( i == 0 )
        {
             if(s[i] >= 'a' && s[i] <= 'z')
            {
                 s[i] = toupper(s[i]);
            }
        }
        else if( s[i] == ' ') //공백이면
        {
            //대문자로
            if( s[i+1] >= 'a' && s[i] <= 'z')
            {
                s[i+1] = toupper(s[i+1]);
            }
        }

    }

    answer = s;

    return answer;
}
```
```
테스트 1 〉	통과 (0.01ms, 4.2MB)
테스트 2 〉	통과 (0.01ms, 4.2MB)
테스트 3 〉	통과 (0.01ms, 4.2MB)
테스트 4 〉	통과 (0.01ms, 4.2MB)
테스트 5 〉	통과 (0.01ms, 3.67MB)
테스트 6 〉	통과 (0.01ms, 4.15MB)
테스트 7 〉	통과 (0.02ms, 3.62MB)
테스트 8 〉	통과 (0.01ms, 4.16MB)    // 드디어 성공 ㅠㅠ
테스트 9 〉	통과 (0.01ms, 4.15MB)
테스트 10 〉	통과 (0.01ms, 3.74MB)
테스트 11 〉	통과 (0.01ms, 3.59MB)
테스트 12 〉	통과 (0.01ms, 4.21MB)
테스트 13 〉	통과 (0.02ms, 3.58MB)
테스트 14 〉	통과 (0.01ms, 4.14MB)
테스트 15 〉	통과 (0.01ms, 3.66MB)
테스트 16 〉	통과 (0.01ms, 3.68MB)
테스트 17 〉	통과 (0.01ms, 4.02MB)
테스트 18 〉	통과 (0.01ms, 4.21MB)
```

***결과는 시간을 단축해야했던 것이었나 보다... 생각보다 문자열끼리 비교하는게 빠른가 보당..***
