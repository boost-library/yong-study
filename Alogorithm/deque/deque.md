## 10866

```python
import sys
from collections import deque

input = sys.stdin.readline

TC = int(input())
queue = deque()
for _ in range(TC):
    cmd = input().split()
    if cmd[0] == "push_front":
        queue.appendleft(cmd[1])
    elif cmd[0] == "push_back":
        queue.append(cmd[1])
    elif cmd[0] == "pop_front":
        if len(queue): print(queue.popleft())
        else: print(-1)
    elif cmd[0] == "pop_back":
        if len(queue): print(queue.pop())
        else: print(-1)
    elif cmd[0] == "size":
        print(len(queue))
    elif cmd[0] == "empty":
        if len(queue) == 0: print(1)
        else: print(0)
    elif cmd[0] == "front":
        if len(queue): print(queue[0])
        else: print(-1)
    elif cmd[0] == "back":
        if len(queue): print(queue[-1])
        else: print(-1)
```

<details>
<summary></summary>

- 일반적인 deque
- if else 삼항연산자 처럼 사용함

</details>

## 1021

```python
from collections import deque

input = sys.stdin.readline

N, M = map(int, input().split())
loc = list(map(int, input().split()))
queue = deque([i for i in range(1, N+1)])

cnt = 0
for i in loc:
    while queue:
        if queue[0] == i:
            queue.popleft()
            break
        else:
            if queue.index(i) < len(queue)/2:
                while queue[0] != i:
                    queue.append(queue.popleft())
                    cnt += 1
            else:
                while queue[0] != i:
                    queue.appendleft(queue.pop())
                    cnt += 1
print(cnt)
```

<details>
<summary></summary>

- 최소, 최대 구분
  2,3번 연산일 떄만 +1
  왼쪽에 가까우면 2번
  오른쪽에 가까우면 3번

- index
  [2,2] -> 첫번쨰 idx 값

</details>
