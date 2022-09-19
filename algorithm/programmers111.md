# [프로그래머스] 프린터 - JavaScript 풀이(개선된 풀이)

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
class Queue {
    constructor() {
        this.queue = [];
        this.front = 0;
        this.rear = 0;
    }
    
    enqueue(value) {
        this.queue[this.rear] = value;
        this.rear += 1;
    }
    
    dequeue() {
        const value = this.queue[this.front];
        delete this.queue[this.front];
        this.front += 1;
        return value;
    }
    
    peek() {
        return this.queue[this.front];
    }
}

function solution(priorities, location) {
    // printer를 Queue 인스턴스로 생성
    const printer = new Queue();
    // priorities의 요소들을 printer에 입력
    priorities.forEach((priority, location) => printer.enqueue({priority, location}));
    
    // priorities를 내림차순으로 정렬
    priorities.sort((a, b) => b - a);
    
    // 인쇄하기
    let printCounter = 0;
    while(true) {
        const currentFront = printer.peek();
        if (priorities[printCounter] > currentFront.priority) {
            printer.enqueue(printer.dequeue());
        } else {
            printer.dequeue();
            printCounter += 1;
            if (currentFront.location === location) {
                break;
            }
        }
    }
    return printCounter;
}
```



## Comment

이전에는 두 개의 배열을 만들어서 복잡하고 깔끔하지 못하게 풀었었는데, Queue 자료형을 배우고 나서 다시 풀어보게 되었다.

직접 Queue 자료형을 Class로 구현하여 풀어내었다.

## Reference

[프로그래머스](https://programmers.co.kr)

