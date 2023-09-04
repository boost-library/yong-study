## bfs dfs

다차원 배열에서 각 칸을 방문할 때 너비를 우선으로 방문하는 알고리즘

좌표를 담을 큐가 필요

1. 시작 → (0,0)에 방문했다는 표시를 남기고 해당 칸을 큐에 넣기
2. 큐가 빌 때까지 계속 큐의 front(0,0)를 뺴고(pop) 해당 좌표의 상하좌우를 살펴보면서 큐에 넣어주는 작업을 반복
3. 큐가 빈 순간 과정은 종료 (0,0)과 상하좌우로 이어진 모든 파란 칸을 방문했음을 확인

---

1. 시작하는 칸을 큐에 넣고 방문했다는 표시를 남김
2. 큐에서 원소를 꺼내어 그 칸을 상하좌우로 인전합 칸에 대해 3번을 진행
3. 해당 칸을 이전에 방문했다면 아무 것도 하지 않고, 처음으로 방문했다면 방문했다는 표시를 남기고 해당 칸을 큐에 삽입
4. 큐의 빌 때까지 2번을 반복

모든 칸이 1번씩 들어가므로 시간복잡도는 칸이 N개일 때 O(N)

큐에서 원소를 뺴고 상하좌우의 칸을 확인하는 식으로 구현

board: 0과 1

vis: 방문처리

상하좌우 방문하는 법

1. 큐의 front를 cur에 저장하고 pop
   ![image](https://github.com/JaeYeopHan/JBEE.io/assets/74396128/5c50087b-ac77-48ac-85b4-6c55ed6f941b)
2. x가 행을, y가 열을

(x,y)에 대해 상하좌우 칸인 (x-1, y), (x, y-1), (x, y+1), (x+1, y)

주로 아래, 오른쪽, 윗쪽, 왼쪽

3. 범위(벽)에 들어오는지 확인
4. 이미 방문했거나 파란칸이 아닌 경우 걸러낸 후 방문 표시(vis[x][y] = 1)

### 자주하는 실수

1. 시작점에 방문했다는 표시를 남기지 않는다 → 시작점을 2번 방문할 수 있음
2. 큐에 넣을 때 방문했다는 표시를 하는 대신 큐에서 빼낼 때 방문했다는 표시를 남김 → 같은 칸이 큐에 여러번 들어가게 되어서 시간 초과나 메모리 초과 발생 가능
3. 이웃한 원소가 범위를 벗어났는지에 대한 체크를 잘못함

![image](https://github.com/JaeYeopHan/JBEE.io/assets/74396128/6b452e20-67cd-415a-9139-77499e33c4b8)

도화지에 있는 모든 그림을 찾아내기 -> 현재 어떤 한 시작점 이어진 그림만 찾아내는 법만 알고있 -> 이중 for문을 돌면서 BFS의 시작점이 될 수 있는 곳을 찾기

(0, 0)은 파란칸이고 아직 방문을 안했으니 여기서 BFS를 시작하면 크기가 4인 그림이 찾아진다. BFS를 돌고나면 방문 표시도 적절하게 남게될 것
![image](https://github.com/JaeYeopHan/JBEE.io/assets/74396128/20eafa96-03a3-4839-8cc3-c79261c0fe82)

2중 for문

그리고 (0,1)이 시작점이 될 수 있는지 보면 (0,1)은 파란칸이지만 이미 방문을 했으니 → BFS를 또 돌리면 ❌

다음은 (0, 2)인데 애초에 빨간 칸이니 걸름

그 다음은 (0, 3)인데 파란칸이고 아직 방문을 하지 않았으니 새로운 그림, → BFS 시작

![image](https://github.com/JaeYeopHan/JBEE.io/assets/74396128/1fde152c-27a4-4206-82e4-8b9e34b32b00)

결국 각 파란칸은 큐에 1번씩만 들어가서 O(N)

위 예시는 Flood Fill 유형

BFS는 다양한 유형을 가지고 있다.

- 다차원 배열에서의 거리측정

  - 미로의 좌측 상단으로부터 우측 하단으로 가는 최단 경로의 길이를 찾는 문제
  - BFS를 이용해 시작점에서 연결된 다른 모든 점으로의 최단 경로를 찾을 수 있음
    ![image](https://github.com/JaeYeopHan/JBEE.io/assets/74396128/43940bc9-1c0e-44fe-8fee-824cf1e9ee6c)

    ![image](https://github.com/JaeYeopHan/JBEE.io/assets/74396128/c961d14b-8a91-44f7-bb5a-7ad2af7a4243)
    빨간색 칸은 현재 칸이고, 검정색 칸은 추가되는 칸 → 이 성질을 사용하면 단순히 상하좌우로 연결된 칸들을 방문하는 것에서 끝나는 것이 아니라, 시작점과의 거리를 전부 계산 가능

    - 거리를 저장할 dist 배열, 상하좌우 칸의 값을 잘봐서 넣어주기
      - 이 배열을 미리 -1로 초기화하면 굳이 vis 배열을 따로 두지 않아도 방문여부 확인 가능

    1. dist 배열 -1로 초기화
    2. 큐 안에서 도는 과정은 vis 대신 dist 사용

### DFS

다차원 배열에서 각 칸을 방문할 때 깊이를 우선으로 방문하는 알고리즘

1. 시작하는 칸을 스택에 넣고 방문했다는 표시를 남김
2. 스택에서 원소를 꺼내어 그 카과 상하좌우로 인접한 칸에 대해 3번을 진행
3. 해당 칸을 이전에 방문했다면 아무 것도 하지 않고, 처음으로 방문했다면 방문했다는 표시를 남기고 해당 칸을 스택에 삽입
4. 스택이 빌 때 까지 2번을 반복

모든 칸일 스택에 1번씩 들어가므로 시간복잡도는 칸이 N개일 떄 O(N)

BFS - 큐(거리순), DFS - 스택(한방향이 막힐 때까지) → 방문순서의 차이

![image](https://github.com/JaeYeopHan/JBEE.io/assets/74396128/ce312f2e-895e-492f-ba90-ccc7ff75bdb8)

다차원 배열에서의 탐색 → BFS 주로 사용, 그래프와 트리에서는 DFS

DFS는 스택을 짜서 다차원 배열의 순회를 처리하는 알고리즘, 깊이를 우선해서 탐색

## 2178

```python
import sys
from collections import deque

input = sys.stdin.readline

n, m = map(int, input().split())

graph = []
for i in range(n):
    graph.append(list(map(int, input().rstrip())))

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

def bfs(x, y):
    queue = deque()
    queue.append((x,y))

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]


            if nx < 0 or nx >= n or ny < 0 or ny >= m: # 범위
                continue
            if graph[nx][ny] == 0: # 이미 방문했거나 그림의 영역이 아닐 경우
                continue
            if graph[nx][ny] == 1: # 1 보다 큰 값은 ❌, 이미 방문한 값
                graph[nx][ny] = graph[x][y] + 1
                queue.append((nx,ny))
    return graph[n-1][m-1]

print(bfs(0,0))
```

```python
import sys
from collections import deque

input = sys.stdin.readline

n, m = map(int, input().split())

graph = []
visited = []
for i in range(n):
    graph.append(list(map(int, input().rstrip())))
    visited.append([-1]*m)

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

def bfs(x, y):
    queue = deque()
    queue.append((x,y))
    visited[x][y] = 0

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if nx < 0 or nx >= n or ny < 0 or ny >= m: # 범위
                continue
            if visited[nx][ny] >= 0 or graph[nx][ny] != 1: # 이미 방문했거나 그림의 영역이 아닐 경우
                continue
            visited[nx][ny] = visited[x][y] + 1
            queue.append((nx,ny))
    return visited[n-1][m-1] + 1

print(bfs(0,0))
```

<details>
<summary></summary>

</details>

### 1926

```python
# 상하좌우로 연결된 그림의 크기를 알아내기 -> 큐에서 pop을 몇 번하는지만 세면
# 도화지에 있는 모든 그림을 찾아내기 -> 현재 어떤 한 시작점 이어진 그림만 찾아내는 법만 알고있 -> 이중 for문을 돌면서 BFS의 시작점이 될 수 있는 곳을 찾기

# 1로 연결된 것을 한 그림이라고 정의
# input: 그림의 개수
# 그림이 하나도 없는 경우에는 가장 넓은 그림의 넓이는 0
import sys
from collections import deque

input = sys.stdin.readline

n, m = map(int, input().split())

# graph = [list(map(int, input().split())) for _ in range(x)]
graph = []
visited = []
for i in range(n):
    graph.append(list(map(int, input().split())))
    visited.append([False]*m)

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

def bfs(x, y):
    init_cnt = 1 # bfs 시작시 누적 방지를 위해 1로 초기화
    queue = deque()
    queue.append((x,y)) # 소관호 튜플 - 수정이 ❌
    visited[x][y] = True # 방문

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if nx < 0 or nx >= n or ny < 0 or ny >= m: # 범위
                continue
            if visited[nx][ny] or graph[nx][ny] != 1: # 이미 방문했거나 그림의 영역이 아닐 경우
                continue
            visited[nx][ny] =True
            queue.append((nx, ny))
            init_cnt += 1

    return init_cnt

cnt, max_cnt = 0,0
for i in range(n):
    for j in range(m):
        if graph[i][j] == 1 and not visited[i][j]:
            cnt +=1 # 그림의 개수
            max_cnt = max(max_cnt, bfs(i,j))
print(cnt)
print(max_cnt)

```

<details>
<summary></summary>

</details>
