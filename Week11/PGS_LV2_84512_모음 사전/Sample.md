# PRO_LV2_84512_모음 사전 [2023.02.24]

https://school.programmers.co.kr/learn/courses/30/lessons/84512

<접근법>

```
- ""부터 뒤에 문자를 하나씩 추가 시키면서(dfs) 입력받은 word랑 같은지 비교한다
- (주의) 추가 시키는 조건을 4이하로 해야한다(5이면 문자 추가를 못한다)
```



```javascript
/**
 * 메모리  : 33.4  KB
 * 시간   : 0.34 ms
 */
function solution(word) {
    // word는 알파벳 대문자 'A', 'E', 'I', 'O', 'U'로 이루어짐
    let chr = ["A","E","I","O","U"];
   // flag 변수
    let Changer = true
    let answer = -1;
   // "" => A => AA => AAA ... DFS 탐색
    function DFS(W){
        if(Changer){
            answer++;
            // 새로 만든 문자열과 word가 같아지면 flag 변수 값 바꾼다 (dfs 종료)
            if(W === word){
                Changer = false;
                return ;
            // word의 길이는 4이하 이거나(5이면 문자 추가 못함) 아직 입력받은 문자열을 완성하지 못하였을 때
            }else if(W !== word && W.length < 5){
            // 문자를 하나씩 추가해서 dfs 돌린다
                for (let i = 0; i < chr.length; i++) {
                    DFS(W + chr[i]);                
                }
            }else{
                return;
            }
        }
    }

    DFS("");

    return answer;
}

```
