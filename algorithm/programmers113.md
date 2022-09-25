# [프로그래머스] 두 큐 합 같게 만들기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
class Queue {
    constructor(array) {
        this.queue = [...array];
        this.front = 0;
        this.rear = array.length;
        this.sum = array.reduce((acc, cur) => acc + cur, 0);
    }
    
    enqueue(value) {
        this.queue[this.rear++] = value;
        this.sum += value;
    }
    
    dequeue() {
        const value = this.queue[this.front];
        delete this.queue[this.front];
        this.front += 1;
        this.sum -= value;
        return value;
    }
}

function solution(array1, array2) {
    let answer = 0;
    // Queue로 변환
    const queue1 = new Queue(array1);
    const queue2 = new Queue(array2);
    // 탐욕법 실행
    const limit =  4 * array1.length;
    while(answer <= limit) {
        if (queue1.sum === queue2.sum) {
            break;
        }
        if (queue1.sum > queue2.sum) {
            queue2.enqueue(queue1.dequeue());
        } else if (queue1.sum < queue2.sum) {
            queue1.enqueue(queue2.dequeue())
        }
        answer += 1;
    }

    return answer > limit ? -1 : answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

