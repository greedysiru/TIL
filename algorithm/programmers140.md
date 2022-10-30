# [프로그래머스]  치킨 쿠폰 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (chicken) => {
    let serviceChicken = 0;
    let restCoupon = 0;
    while (chicken > 0) {
        restCoupon += chicken % 10;
        chicken = Math.floor(chicken / 10);;
        serviceChicken += chicken;
        if (restCoupon >= 10) {
            const restCouponChicken = Math.floor(restCoupon / 10);
            restCoupon -= restCouponChicken * 10;
            serviceChicken += restCouponChicken; 
            chicken += restCouponChicken
        }
    }
    return serviceChicken;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

