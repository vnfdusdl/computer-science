### 스택(stack)

LIFO(Last In First Out) 형태로 한 쪽 끝에서만 자료를 넣고 빼는 작업이 이루어지는 자료구조

- 서로 관계가 있는 여러 작업을 연달아 수행하면서 이전의 작업 내용을 저장해 둘 필요가 있을 때 널리 사용된다.
- `top` : 가장 최근에 스택에 삽입된 자료의 위치
- 스택의 맨 위 요소, `top`에만 접근이 가능하기 때문에 `top`이 아닌 위치의 데이터에 대한 접근, 삽입, 삭제는 모두 불가능하다.
- `stack overflow` : 꽉 찬 스택에 `stack.push`를 시도하는 것
- `stack underflow` : 스택이 비어있을 때 `stack.pop`을 시도하는 것
- 
```javascript
class Stack {
  constructor() {
    this._arr = [];
  }
  push(item) {
    this._arr.push(item);
  }
  pop() {
    return this._arr.pop();
  }
  peek() {
    return this._arr[this._arr.length - 1];
  }
}

const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);
stack.pop(); // 3
```

**시간 복잡도**

- 삽입 : O(1)
- 제거 : O(1)
- 탐색 : O(N)
- 접근 : O(N)

**스택 주요 동작**

- 삭제 (pop()) : 스택에서 가장 위에 있는 항목을 제거한다. [O(1)]
- 삽입 (push(item)) : item 하나를 스택의 가장 윗부분에 추가한다. [O(1)]
- 읽기 (peek()) : 스택의 가장 위에 있는 항목을 반환한다. [O(1)]

**장단점**

- `top` 을 통해 접근하기 때문에 데이터 접근, 삽입, 삭제가 빠르다
- `top` 위치 이외의 데이터에 접근할 수 없기 때문에 탐색이 불가능하다. 탐색하려면 모든 데이터를 꺼내면서 진행해야 한다.

**스택의 활용 예시**

스택의 특징인  후입선출(LIFO)을 활용하여 여러 분야에서 활용 가능하다.

- 웹 브라우저 방문기록 (뒤로 가기) : 가장 나중에 열린 페이지부터 다시 보여준다.
- 역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력한다.
- 실행 취소 (undo) : 가장 나중에 실행된 것부터 실행을 취소한다.
- 후위 표기법 계산
- 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)
- 재귀 알고리즘
- DFS 알고리즘
