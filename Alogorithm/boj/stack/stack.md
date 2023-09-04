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

# 스택의 활용(수식의 괄호 쌍)

1. 여는 괄호가 나오면 스택에 추가
2. 닫는 괄호가 나왔을 경우,
   a. 스택이 비어있으면 올바르지 않은 괄호 쌍
   b. 스택의 top이 짝이 맞지 않는 괄호일 경우 올바르지 않는 괄호 쌍
   c. 스택의 top이 짝이 맞는 괄호일 경우 pop
3. 모든 과정을 끝낸 후 스택에 괄호가 남아있다면 올바르지 않은 괄호 쌍, 남아있지 않으면 올바른 괄호 쌍

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

## 4949

```python
import sys

input = sys.stdin.readline

while True:
    s = input().rstrip()
    stack = []
    check = True

    for char in s:
        if char == "(" or char == "[":
            stack.append(char)
        elif char == ")":
            if stack and stack[-1] == "(":
                stack.pop()
            else:
                check = False
                break
        elif char == "]":
            if stack and stack[-1] == "[":
                stack.pop()
            else:
                check = False
                break

    if s == ".":
        break
    print("yes" if check and not stack else "no")
```

<details>
<summary></summary>

- `"."`은 입력의 마지막을 의미하는 조건

- rtrip()
- lstrip()
- strip()

</details>

## 3986

```python
import sys

input = sys.stdin.readline

TC = int(input())
cnt = 0
for i in range(TC):
    s = input().rstrip()
    stack = []
    for char in range(len(s)):
        if stack and stack[-1] == s[char]:
            stack.pop()
        else: stack.append(s[char])
    if not stack: cnt +=1
print(cnt)
```

<details>
<summary></summary>

</details>

## 9012

```python
import sys

input = sys.stdin.readline

TC = int(input())
cnt = 0
for _ in range(TC):
    s = input().rstrip()
    stack = []
    check = True

    for char in s:
        if char == "(":
            stack.append(char)
        elif char == ")":
            if stack and stack[-1] == "(":
                stack.pop()
            else:
                check = False
                break
    print("YES" if check and not stack else "NO")
```

<details>
<summary></summary>

</details>

## 10799

```python
import sys

input = sys.stdin.readline

s = input().rstrip()
stack = []
cnt = 0
for i in range(len(s)):
    if s[i] == "(":
        stack.append("(")
    else:
        if s[i - 1] == "(":
            stack.pop()
            cnt += len(stack)

        else:
            stack.pop()
            cnt += 1
print(cnt)
```

<details>
<summary></summary>

닫히는 괄호에서의 분기점

- "("가 나온다면 현재까지의 쇠파이프("(")를 더해주기
- ")"가 나온다면 새로 생긴 쇠파이프 1개를 더해주기

</details>

## 2504

```python
import sys
input = sys.stdin.readline

bracket = input().rstrip()
stack = []
res = 0
tmp = 1

for i in range(len(bracket)):

    if bracket[i] == "(":
        stack.append(bracket[i])
        tmp *= 2

    elif bracket[i] == "[":
        stack.append(bracket[i])
        tmp *= 3

    elif bracket[i] == ")":
        if not stack or stack[-1] == "[":
            res = 0
            break
        if bracket[i-1] == "(":
            res += tmp
        stack.pop()
        tmp //= 2

    else:
        if not stack or stack[-1] == "(":
            res = 0
            break
        if bracket[i-1] == "[":
            res += tmp

        stack.pop()
        tmp //= 3

if stack:
    print(0)
else:
    print(res)
```

<details>
<summary></summary>

꺼낸 괄호가 닫는 괄호일 떄, 그 괄호의 직전의 괄호와 쌍이 맞는 경우에만 곱한다(res에 더하기 수행)

</details>
