# 스택의 성질

한 쪽 끝에서만 원소를 넣거나 뺄 수 있는 자료구조

FILO, LILO

큐, 덱, 스택 → 특정 위치에서만 원소를 넣거나 뺼 수 있는 제한이 걸려있다 → Restricted Structure

1. 원소의 추가 O(1)
2. 원소의 제거 O(2)
3. 제일 상단의 원소 확인 O(1)
4. 제일 상단이 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능

활용 알고리즘

수식의 괄호 쌍, DFS, Flood Fill 등

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