# [프로그래머스]  스킬트리 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(skill, skill_trees) {
    let answer = 0;
    // skill_trees 순회
    for (let i = 0; i < skill_trees.length; i++){
        const skillTree = skill_trees[i];
        let flag = true;
        // 배워야하는 스킬 인덱스
        let skillIndex = 0;
        for (let j = 0; j < skillTree.length; j++) {
            // 현재 접근한 스킬 인덱스
            const currentSkillIndex = skill.indexOf(skillTree[j]);
            if (currentSkillIndex === skillIndex) {
                skillIndex += 1;
            }
            else if (currentSkillIndex > 0 && currentSkillIndex !== skillIndex) {
                flag = false;
                break;
            }
        }
        if (flag) {
            answer += 1;
        }
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

