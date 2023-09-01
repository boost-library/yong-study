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

## 5397

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

## 10773

```python
import sys

input = sys.stdin.readline

TC = int(input())
for i in range(TC):
    cmd = input().rstrip()
    lStack = [];
    rStack = [];
    for j in cmd:
        if j == '<':
            if lStack: rStack.append(lStack.pop())
        elif j == '>':
            if rStack: lStack.append(rStack.pop())
        elif j == '-':
            if lStack: lStack.pop()
        else: lStack.append(j)
    # print(lStack, reversed(rStack), ''.join(lStack.extend(reversed(rStack))))
    print("".join(lStack) + "".join(rStack[::-1]))
```

<details>
<summary></summary>

- 리스트를 합치는 다양한 방법
  - ret = a + b
  - `a.append(b)`
  - b의 원소가 그대로 하나의 값으로 추가 됨
    - a = [1, 2, 3], b = [[4, 5]] -> a = [1, 2, 3, [4, 5]]
    - a = [1, 2, 3], b = ['hi'] -> a = [1, 2, 3, 'hi]
  - `a.extend(b)`
  - iterable 요소 하나하나가 개별로 추가
    - a = [1, 2, 3], b = [[4,5]] -> a = [1, 2, 3, 4, 5]
    - b = [1, 2, 3], b = ['hi'] -> a = [1, 2, 3, 'h', 'i']

</details>
