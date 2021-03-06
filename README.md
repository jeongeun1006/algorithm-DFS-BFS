# algorithm-DFS-BFS
## 음료수 얼려 먹기

#### 설명

+ N x M 크기의 얼음 틀이 있다. 구멍이 뚫려있는 부분은0, 칸막이가 존재하는 부분은 1로 표시한다. 구멍이 뚫려있는 부분(0)이 상,하,좌,우로 붙어 있는 경우 서로 연결되어 있는 것으로 간주하고 1개의 아이스크림으로 만든다. 

#### 입력
+ 첫 번째 줄에 얼음 틀의 세로길이 N과 가로길이 M 을 입력한다
+ 두 번째 줄부터 얼음틀의 형태를 입력한다.

#### 출력
+ 한 번에 만들 수 있는 아이스크림의 개수를 출력

----------

#### 코드 리뷰

+ 이 문제는 DFS 로 해결 할 수 있다.
1. 특정한 지점의 주변 상,하,좌,우를 살펴본 뒤에 주변 지점 중에서 값이 0이면서 아직 방문하지 않은 지점이 있다면 해당 지점을 방문한다
2. 방문한 지점에서 다시 상,하,좌,우를 살펴보면서 방문을 다시 진행하면, 연결된 모든 지점을 방문할 수 있다
3. 1~2번의 과정을 모든 노드에 반복하며 방문하지 않은 지점의 수를 센다

+ DFS로 특정한 노드를 방문한 뒤에 연결된 모든 노드들도 방문
```python
def dfs(x,y):
  if x<=-1 or x>=n or y<=-1 or y>=n:
    return False
  if graph[x][y]==0:
    graph[x][y]=1
    dfs(x-1,y)
    dfs(x+1,y)
    dfs(x,y-1)
    dfs(x,y+1)
    return True
  return False
  ```
  만약 주어진 범위를 벗어나는 경우에는 즉시 종료
  
  만약 현재 노드를 아직 방문하지 않았다면(0이라면) 해당노드를 방문처리 해주고 상,하,좌,우의 위치도 모두 재귀적으로 호출한다.
  
  --------
  + 모든 노드(위치)에 대하여 음료수 채우기
  ```python
  for i in range(n):
    for j in range(m):
      if dfs(i,j)==True:
        result+=1
  ```
  
  --------
  
  ## 미로 탈출
  
  
  #### 설명 
  
  + N X M 크기의 직사각형 형태의 미로에서 탈출해야 한다. 현재 위치는 (1,1) 이고 미로의 출구는 (N,M)의 위치에 존재하며 한 번에 한 칸씩 이동할 수 있다. 0은 벽이며 1로 표시된 부분만 움직일 수 있다. 미로를 탈출하기 위한 최소 칸의 개수를 구해야 한다.
  
  #### 입력
  
  + 첫째 줄에 N,M 크기의 미로 입력. 다음 줄 부터는 미로의 정보 입력. 시작칸과 마지막 칸은 항상 1
  
  #### 출력
  
  + 최소 이동 칸의 개수를 출력
  
  ------
  
  #### 코드 리뷰
  
  1. 이 문제는 BFS 를 이용 했을 때 효과적으로 해결 가능하다.
  - BFS는 시작지점에서 가까운 노드부터 차례대로 그래프의 모든 노드를 탐색하기 때문
  2. 특정한 노드를 방문하면 그 이전 노드의 거리에 1을 더한 값을 리스트에 넣는다
  
  + BFS 소스코드 구현
  
  ```python
  def bfs(x,y):
  queue=deque()
  queue.append((x,y))
  while queue:
    x,y=queue.popleft()
    for i in range(4):
      nx=x+dx[i]
      ny=y+dy[i]
      if nx<0 or ny<0 or nx>=n or ny>=m:
        continue
      if graph[nx][ny]==0:
        continue
      if graph[nx][ny]==1:
        graph[nx][ny]=graph[x][y]+1
        queue.append((nx,ny))
  return graph[n-1][m-1]
  ```
  +큐가 빌 때까지 반복한다
  
  + 해당 노드를 처음 방문하는 경우에만 최단 거리를 기록한다
  
  
