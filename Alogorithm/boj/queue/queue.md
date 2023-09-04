## 큐

### 큐의 성질

1. 원소의 추가 O(1)
2. 원소의 제거 O(1)
3. 제일 앞/뒤 원소 확인 O(1)
4. 제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능

스택에서는 보통 원소가 추가되는 곳을 top, 원소가 위 아래로 배치되는 것으로 생각

## 18258

```python
import sys
from collections import deque

input = sys.stdin.readline

TC = int(input())
queue = deque()
for t in range(TC):
    cmd = input().split()
    if cmd[0] == "push":
        queue.append(cmd[1])
    elif cmd[0] == "pop":
        if len(queue): print(queue.popleft())
        else: print(-1)
    elif cmd[0] == "size":
        print(len(queue))
    elif cmd[0] == "empty":
        if len(queue): print(0)
        else: print(1)
    elif cmd[0] == "front":
        if len(queue): print(queue[0])
        else: print(-1)
    elif cmd[0] == "back":
        if len(queue):
            print(queue[-1])
        else: print(-1)
```

## 2164

```python
import sys
from collections import deque

input = sys.stdin.readline

TC = int(input())
queue = deque()
# dq = deque(maxlen=n)

for i in range(TC):
    queue.append(i+1)

while(len(queue) !=1):
    queue.popleft()
    queue.append(queue.popleft())
print(queue[0])
```

<details>
<summary></summary>

- Doubly Ended Queue
- deque 이중 연결리스트 아래와 같이 구현되어 있다.

```python
typedef struct BLOCK {
    struct BLOCK *leftlink;
    PyObject *data[BLOCKLEN];
    struct BLOCK *rightlink;
} block;

+
−typedef struct {
    PyObject_VAR_HEAD
    block *leftblock;
    block *rightblock;
    Py_ssize_t leftindex;       /* 0 <= leftindex < BLOCKLEN */
    Py_ssize_t rightindex;      /* 0 <= rightindex < BLOCKLEN */
    size_t state;               /* incremented whenever the indices move */
    Py_ssize_t maxlen;
    PyObject *weakreflist;
} dequeobject;
```

- 3항 연산자

```python
elif cmd[0] == "pop_front":
print(dq.popleft() if dq else -1)
```

- deque에 maxlen 설정가능

</details>
