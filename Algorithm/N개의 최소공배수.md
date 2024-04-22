## 프로그래머스 Lv 2 N개의 최소 공배수 
최소 공배수 문제를 풀 때 어떻게 하면 가장 빠르게 문제를 풀까 고민했다.
나름 아이디어를 써서 소인수 분해도 하였다.

유클리드 호제법 이라는 최대 공약수 알고리즘도 있지만 여러 개의 문제를 고려해서 문제를 풀어야 할 때에도 있기 때문에 나름 아이디어를 짜보았지만
가장 코드가 보기 깔끔한건 유클리드 호제법을 사용하는 게 낫지 않나 싶다.

### 문제 설명
두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 
예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다.
n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

### 제한 사항
- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

### 입출력 예
| arr | 	result |
| --- | --- |
| [2,6,8,14] |	168 |
| [1,2,3] |	6 |

### 문제 풀이 1
```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int solution(vector<int> arr) {
    
    sort(arr.begin(), arr.end(), less<>());
    
    for(int i = 0; i < arr.size(); i++)
    {
        if( arr[i] == 1 )
            continue;
        
        for(int j = 0; j < arr.size(); j++ )
        {
            
            if( i != j && arr[j] % arr[i] == 0)
            {
                arr[j] = arr[j] / arr[i];
            }
        }
        
    }
    
    int answer = arr[0];

    for(int i = 1; i < arr.size(); i++)
    {
        answer *= arr[i];
    }

    
    return answer;
}
```
처음엔 그냥 공약수를 찾아서 제거했고 남은 공약수끼리 곱하면 최소 공배수가 나오기 때문에 이렇게 진행했습니다.
하지만, 답은 맞추었지만 결과적으로 정확성 테스트에서 실패하였습니다.
예상 가는 것은 arr[j] = arr[j] / arr[i] 이 부분에서 arr[i]로 즉, 배열에 있는 수로 계산해서 인 것 같았습니다.

이후 이 방법 말고 풀이를 생각해보았습니다.

### 문제 풀이 2
```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <map>

using namespace std;

int solution(vector<int> arr) {
    
    sort(arr.begin(), arr.end(), less<>());
    
    vector<vector<int>> vFactorization;
    
   //소인수 분해
   for(int i = 0; i < arr.size(); i++)
   {
       vector<int> factorization;
       int nTemp = 2;
       while( arr[i] != 1 )
       {
            if( arr[i] % nTemp == 0 )
            {
                arr[i] /= nTemp;
                factorization.push_back(nTemp);
            }
            else
            {
                nTemp++;
            }
       }
       
       vFactorization.push_back(factorization);
   }
    
    bool bFlag = false;
   for(int i = 0; i < vFactorization.size(); i++ )
   {
       for( int j = i; j < vFactorization.size(); j++ )
       {
           for( int k = 0; k < vFactorization[i].size(); k++ )
           {
               bFlag = false;
               
               for( int l = 0; l < vFactorization[j].size(); l++)
               {
                   if( bFlag == true ) break;
                   
                    if( i != j && vFactorization[i][k] == vFactorization[j][l])
                    {
                        vFactorization[j][l] /= vFactorization[i][k];
                        bFlag = true;
                    }
               }
           }
       }
   }
    
    int answer = 1;
    for(int i = 0; i < vFactorization.size(); i++ )
    {
        vector<int> factorization = vFactorization[i];
        for(int j = 0; j < factorization.size(); j++)
        {
            answer *= factorization[j];
        }
    }

    
    return answer;
}
```
생 노가다 같은 코드로 풀어보니 일일이 소인수 분해하여 소인수 분해한 자료를 비교하여 최소 공배수를 찾아 최소 공배수를 제외한 나머지 값들끼리 계산을 해주니
정확성 테스트에서도 완전히 통과되었습니다.

하지만!!

누가봐도 꼴보기 싫은 저 4중 for문....과 flag를 이용하여 나름 구분하려고 했지만 가독성이 현저히 떨어지는 코드를 보고 있자니 다른 사람 코드들을 분석해보기로 했습니다.

### 문제 풀이 3
```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int gcd(int a, int b)
{
	int c;
	while( b != 0 )
	{
		c = a % b;
		a = b;
		b = c;
	}
	
	return a;
}

int solution(vector<int> arr) {
    
    sort(arr.begin(), arr.end(), less<>());
    int answer = arr[0];
    
    for(int i = 1; i < arr.size(); i++)
    {
        arr[i] /= gcd(answer, arr[i]);
        answer *= arr[i];
		  //answer = answer * arr[i] / gcd(answer, arr[i]);   //위에 코드를 풀어보면 주석과 같다.
		
    }
    
    return answer;
}
```
두번째는 유클리드 호제법을 이용하여 최대 공약수를 구하여 최대 공배수를 구하는 방법이다.

### 함수로 코드 정리
```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int gcd(int a, int b)
{
	int c;
	while( b != 0 )
	{
		c = a % b;
		a = b;
		b = c;
	}
	
	return a;
}

int lcm(int a , int b)
{
    return a * b / gcd(a, b);
}

int solution(vector<int> arr) {
    
    sort(arr.begin(), arr.end(), less<>());
    int answer = arr[0];
    
    for(int i = 1; i < arr.size(); i++)
    {
        answer = lcm(answer, arr[i]);
    }
    
    return answer;
}
```
더 가독성을 높이면 이렇게 된다....
유클리드 호제법... 알고리즘이 편하긴 하다


