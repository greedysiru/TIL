# [프로그래머스]  배상 비용 최소화 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
class MaxHeap {
    constructor() {
        this.heap = [null];
    }
    
    push(value) {
        this.heap.push(value);
        let currentIndex = this.heap.length - 1;
        let parentIndex = Math.floor(currentIndex / 2);
        
        while (parentIndex !== 0 && this.heap[parentIndex] < value) {
            const temp = this.heap[parentIndex];
            this.heap[parentIndex] = value;
            this.heap[currentIndex] = temp;
            
            currentIndex = parentIndex;
            parentIndex = Math.floor(currentIndex / 2);
        }
    }
    
    pop() {
        const returnValue = this.heap[1];
        if (this.heap.length === 2) {
            this.heap = [null];
            return returnValue;
        }
        this.heap[1] = this.heap.pop();
        let currentIndex = 1;
        let leftIndex = 2;
        let rightIndex = 3;
        
        while (
            this.heap[currentIndex] < this.heap[leftIndex] ||
            this.heap[currentIndex] < this.heap[rightIndex]
        ) {
            if (this.heap[leftIndex] < this.heap[rightIndex]) {
                const temp = this.heap[currentIndex];
                this.heap[currentIndex] = this.heap[rightIndex];
                this.heap[rightIndex] = temp;
                currentIndex = rightIndex;
            } else {
                const temp = this.heap[currentIndex];
                this.heap[currentIndex] = this.heap[leftIndex];
                this.heap[leftIndex] = temp;
                currentIndex = leftIndex;
            }
            leftIndex = currentIndex * 2;
            rightIndex = currentIndex * 2 + 1;
        }
        return returnValue;
    }
}

function solution(no, works) {
    var result = 0;
    // maxHaep 생성
    const maxHeap = new MaxHeap();
    works.forEach(work => maxHeap.push(work));
    
    // 배상 비용이 최소화되도록 순회여 처리
    for (let i = 1; i <= no; i++) {
        // 작업량이 가장 큰 요소를 가져오기
        const maxWork = maxHeap.pop();
        // maxWork가 0인경우, 중단
        if (maxWork === 0) {
            break;
        }
        // 작업량을 -1한 후, 다시 넣기
        maxHeap.push(maxWork - 1);
    }
    // 답 구하기
    return maxHeap.heap.reduce((acc, cur) => acc + cur ** 2, 0);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

