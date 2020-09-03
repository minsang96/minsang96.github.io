---
title: "[프로그래머스] 보석 쇼핑 - C++"
date: 2020-09-03 22:35:28 -0400
categories: 코딩테스트
---
투포인터의 개념을 정확히 모르고 풀었는데, 계속 특정 문제에서만 실패가 떠서 시간을 오래 잡아 먹은 문제였다. 오류의 원인은 else if(e == gems.size()) 부분을 if(e == gems.size())라고 써버리는 바람에 e값이 gems.size()가 되자마자 s가 증가하면서 distance가 작아질 기회를 없애버렸기 때문이였다..

```c++
#include <string>
#include <vector>
#include <map>

using namespace std;

vector<int> solution(vector<string> gems) {
    vector<int> answer = {1, (int)gems.size()}; // 인덱스를 직접 참조하여 값을 수정하기 위해 초기값을 설정  
    int s = 0; //start 
    int e = 0; //end
    int distance = gems.size()-1; // end-start의 값으로 가장 작은 구간을 구하기 위한 변수
    map<string, int> m;
    int total;
    for(string i : gems) {
        m[i] += 1;
    }
    
    total = m.size(); // 보석의 갯수를 구한 뒤
    m.clear(); // 맵 초기화
    
    while(true) {
        if(m.size() == total) { // 모든 보석을 다 구한 경우
            if(e-s<distance) { // end-start(현재구간)과 distance(미리 구해놨던 최단구간)를 비교
                distance = e-s;
                answer[0] = s+1;
                answer[1] = e;
            }
            
            if(m[gems[s]] == 1) { // 보석의 갯수가 1개 일 때
                m.erase(gems[s]);
                s++; // m[gems[s]]가 1일때 --을 하면 맵에서 사라지지 않고 value가 0이 되기 때문
            }
            else { // 보석의 갯수가 1개 이상일 때
                m[gems[s]]--;
                s++;
            }
        }
        else if(e == gems.size()) // 끝까지 탐색을 마쳤을때
            break;
        
        else { // 모든 보석을 아직 찾지 못했을 경우
                m[gems[e]]++;
                e++; // end값을 증가시키면서 gems[e]에 해당하는 보석의 갯수 증가
        }
        
    }
    
    return answer;
}
}

```
https://velog.io/@minsang96/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EB%B3%B4%EC%84%9D-%EC%87%BC%ED%95%91-C

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
