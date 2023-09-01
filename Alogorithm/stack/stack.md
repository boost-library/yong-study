## 10828

```python
import sys

input = sys.stdin.readline

TC = int(input())
stack = []
for t in range(TC):
    cmd = input().split()
    if cmd[0] == "push":
        stack.append(cmd[1])
    elif cmd[0] == "top":
        if len(stack) == 0: print(-1)
        else: print(stack[-1])
    elif cmd[0] == "pop":
        if len(stack) == 0: print(-1)
        else: print(stack.pop())
    elif cmd[0] == "empty":
        if len(stack) == 0: print(1)
        else: print(0)
    else: print(len(stack))
```

<details>
<summary></summary>

</details>

## 10773

```python
import sys

input = sys.stdin.readline

TC = int(input())
stack = []
for _ in range(TC):
    cmd = int(input())
    if cmd == 0:
        if stack:
            stack.pop()
    else: stack.append(cmd)

print(sum(stack))
```

<details>
<summary></summary>

- `k: int = int(input().rstrip())` 타입 지정 가능 3.5이상 부터
- `stack.pop() if num==0 else stack.append(num)` 3항 연산자 구현 가능

</details>
