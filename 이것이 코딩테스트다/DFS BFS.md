# 깊이 우선탐색, 너비우선탐색

보통 DFS는 스택 사용, BFS는 큐 사용,

코테에서는 보통 BFS가 DFS보다 빠르게 동작한다.

# 음료수 얼려 먹기

```javascript
function solution(arr) {
  const dx = [-1, 0, 1, 0];
  const dy = [0, 1, 0, -1];
  let answer = 0;
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr[0].length; j++) {
      if (arr[i][j] == 0) {
        DFS(i, j);
        answer++;
      }
    }
  }
  return answer;

  //상,우,하,좌
  function DFS(x, y) {
    arr[x][y] = 1;
    for (let i = 0; i < 4; i++) {
      if (
        x + dx[i] < arr.length &&
        x + dx[i] >= 0 &&
        y + dy[i] < arr[0].length &&
        y + dy[i] >= 0
      ) {
        if (arr[x + dx[i]][y + dy[i]] == 0) {
          DFS(x + dx[i], y + dy[i]);
        }
      }
    }
  }
}

console.log(
  solution([
    [0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0],
    [1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 0],
    [1, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 1, 0],
    [1, 1, 0, 1, 1, 1, 0, 1, 1, 0, 0, 0, 0, 0],
    [1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
    [1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0],
    [1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
    [1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
  ])
);
// console.log(
//   solution([
//     [0, 0, 1, 1, 0],
//     [0, 0, 0, 1, 1],
//     [1, 1, 1, 1, 1],
//     [0, 0, 0, 0, 0],
//   ])
// );
```

책에서 난이도는 1.5에 제한시간 30분이라고 써있길래 이걸 30분안에 풀수있을까? 싶었는데 30분내로 풀었다. 물론 이전에 거의 동일한 [섬,육지 문제](<https://github.com/MoonEunki/algorithm/blob/main/%EA%B0%95%EC%9D%98/%EA%B7%B8%EB%9E%98%ED%94%84%EC%99%80%20%ED%83%90%EC%83%89(DFS%2C%20BFS)/7.%20%EC%84%AC%EB%82%98%EB%9D%BC%20%EC%95%84%EC%9D%BC%EB%9E%9C%EB%93%9C(DFS).md>)를 풀어봤기 때문이긴하지만 어쨌든 굉장히 뿌듯했음.

# 미로 탈출

```javascript
function solution(map) {
  // 상 우 하 좌
  const dx = [-1, 0, 1, 0];
  const dy = [0, 1, 0, -1];
  const queue = [[0, 0]];

  while (queue.length) {
    const [x, y] = queue.shift();
    for (let i = 0; i < 4; i++) {
      let nx = x + dx[i];
      let ny = y + dy[i];
      if (nx < 0 || nx >= map.length || ny < 0 || ny >= map[0].length) continue;
      if (map[nx][ny] === 0) continue;
      if (map[nx][ny] === 1) {
        map[nx][ny] = map[x][y] + 1;
        queue.push([nx, ny]);
      }
    }
  }

  return map[map.length - 1][map[0].length - 1];
}

console.log(
  solution([
    [1, 0, 1, 0, 1, 0],
    [1, 1, 1, 1, 1, 1],
    [0, 0, 0, 0, 0, 1],
    [1, 1, 1, 1, 1, 1],
    [1, 1, 1, 1, 1, 1],
  ])
);
```

로직상엔 문제가없는거같은데 답이 이상하게나와서 머리가 아팠는데, 멍청하게 시작 좌표를 0,0으로 안하고 1,1로 해서 헤맸다..
