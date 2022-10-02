# [프로그래머스] 가장 먼 노드 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
// Queue 구현
class Queue {
    constructor() {
        this.queue = [];
        this.front = 0;
        this.rear = 0;
    }
    
    enqueue(value) {
        this.queue[this.rear++] = value;
    }
    
    dequeue() {
        const value = this.queue[this.front];
        delete this.queue[this.front];
        this.front += 1;
        return value;
    }
    
    isEmpty(){
        return this.rear === this.front;
    }
}

function solution(n, edge) {
    // 트리 만들기
    const tree = [[]];
    edge.forEach(vertex => {
        tree[vertex[0]] = tree[vertex[0]]? [...tree[vertex[0]], vertex[1]]  : [vertex[1]];
        tree[vertex[1]] = tree[vertex[1]]? [...tree[vertex[1]], vertex[0]]  : [vertex[0]];
    });
    // 거리를 기록할 배열
    const distances = new Array(n + 1).fill(0);
    distances[1] = 1;
    // 최대 거리
    let maxDistnace = 0;
    
    const queue = new Queue();
    queue.enqueue(1);
    while (!queue.isEmpty()) {
        const currentNode = queue.dequeue();
        // tree의 경로를 탐색
        for (const node of tree[currentNode]){
            if (distances[node] === 0) {
                queue.enqueue(node);
                distances[node] += distances[currentNode] + 1;
                if (maxDistnace < distances[node]) maxDistnace = distances[node];
            }
        }
    }
    return distances.filter( e => e === maxDistnace).length;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

