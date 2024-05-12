## Blocking/Non-Blocking

Blocking과 Non-Blocking은 `호출된 함수`가 `호출한 함수`에게 제어권을 바로 주느냐 안주느냐의 차이이다.

함수 A, 함수 B가 존재하고, A가 B를 호출했다고 가정해보자. 이때 호출한 함수는 A이고, 호출된 함수는 B이다. 현재 B가 호출되면서 B는 자신의 일을 수행해야한다. (제어권이 B에게 주어진 상황)

- **Blocking**

    <aside>
    함수 B가 본인의 할일을 모두 마칠 때까지 제어권을 가지고 있는다. A는 B의 업무가 끝날 때까지 기다려야한다.
    </aside>

  ```
  치즈🧀: 감자🥔님 결재 올렸습니다.
  감자🥔: 네 감자🥔님 서류 읽을 때까지 기다리고 계세요. (치즈🧀 다른일 못함)

  (.. 서류 검토 중)

  감자🥔: 다 읽었으니 나가보세요. (치즈🧀 다른 일 할 수 있음)
  ```

- **Non-Blocking**

    <aside>
    함수 B가 제어권을 바로 함수 A에게 넘겨주면서, 함수 A가 다른 일을 할 수 있도록 한다.
    
    즉, 다른 주체의 작업에 관련없이 자신의 작업을 수행하는 것을 의미한다. 
    </aside>

  ```
  치즈🧀: 감자🥔님 결재 올렸습니다.
  감자🥔: 네 서류 두고 가세요. (치즈🧀 다른 일 할 수 있음)
  ```

<br>

## Synchronous/Asynchronous

<img src="https://media.vlpt.us/images/effypark/post/0aee939b-c9f0-4b6c-a4ca-aa7de823245e/image.png">

Blocking과 Non-Blocking은 호출된 함수의 종료를 `호출한 함수`가 처리하느냐, `호출된 함수`가 처리하느냐의 차이이다.

함수 A, 함수 B가 존재할 때, 호출된 함수 B의 수행 결과나 종료 상태를 호출된 함수 A가 신경쓰고 있는 유무의 차이를 확인하면 된다.

- **Synchronous (동기)**

    <aside>
    함수 A는 함수 B가 일을 하는 중에 기다리면서, 현재 상태가 어떤지 계속 체크한다.
    
    즉, 작업을 동시에 수행하거나, 동시에 끝나거나, 끝나는 동시에 시작함을 의미한다. 
    </aside>

  ```
  치즈🧀: 감자🥔님 결재 올렸습니다.
  감자🥔: 네, 치즈🧀님 기다리셔도 되고, 다른 일을 하고 계셔도 돼요.

  (... 결재 검토 중)

  치즈🧀: 감자🥔님 결재 내용 수정되었습니다.
  감자🥔: 네, 치즈🧀님 수정 사항 반영해서 검토하겠습니다.

  ```

- **Asynchronous (비동기)**

    <aside>
    함수 B의 수행 상태를 B 혼자 신경쓰면서 처리한다.
    
    즉, 시작, 종료가 일치하지 않으며, 끝나는 동시에 시작하지 않음을 의미한다.

  비동기는 호출 시 Callback을 전달하여 작업의 완료 여부를 호출한 함수에게 답한다. (Callback이 오기 전까지 호출한 함수는 신경쓰지 않고 다른 일을 할 수 있음)
    </aside>

  ```
  치즈🧀: 감자🥔님 결재 올렸습니다.
  감자🥔: 네, 치즈🧀님 기다리셔도 되고, 다른 일을 하고 계셔도 돼요.

  (... 결재 검토 중)

  치즈🧀: 감자🥔님 결재 내용 수정되었습니다.
  감자🥔: 네, 치즈🧀님 수정 사항은 언젠가 내용을 확인하고 처리하도록 하겠습니다.

  ```

- **Pros and Cons**

  Synchronous

  ```
  🙂 설계가 매우 간단하다. 직관적이다.
  😕 결과가 주어질 때까지 아무것도 못하고 대기해야 한다.
  ```

  Asynchronous

  ```
  🙂 결과가 주어지기 전에도 다른 작업을 할 수 있다. 자원을 효율적으로 사용할 수 있다.
  😕 Synchronous보다 설계가 복잡하다. 덜 직관적이다.
  ```

## 4가지 Case

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fda50Yz%2Fbtq0Dsje4ZV%2FlGe8H8nZgdBdgFvo7IczS0%2Fimg.png">

- Blocking: [기다림] 호출된 함수는 작업이 끝나야 호출한 함수에게 제어권을 리턴해준다.
- Non-Blocking: [안 기다림] 호출된 함수는 제어권을 호출한 함수에게 바로 리턴해준다.
- Synchronous: [내가 함] 호출한 함수는 호출된 함수의 응답을 받아야 다음 동작을 실행한다.
- Asynchronous: [다른 사람 시킴] 호출한 함수는 호출된 함수의 응답과 관계없이 다음 동작을 실행한다.

### 1. Blocking + Synchronous

```
1. [동기적 업무 지시] 팀장님이 사원1에게 업무 A를 지시하고, 사원1의 업무를 마칠 때까지 대기한다.

2. [blocking 방식의 작업 처리] 사원1이 업무 A를 완료할 때까지 팀장님이 대기한다.

3. [동기적 업무 지시] 팀장님이 사원2에게 업무 B를 지시하고, 사원2의 업무를 마칠 때까지 대기한다.

4. [blocking 방식의 작업 처리] 사원2가 업무 B를 완료할 때까지 팀장님이 대기한다.
```

### 2. Blocking + Asynchronous

```

1. [비동기적 업무 지시] 팀장님이 사원1에게 업무 A를, 사원2에게 업무 B를 지시하고 싶었지만 ..

2. [Blocking 방식의 작업 처리] 사원1이 자신의 일이 끝날 때까지 팀장님을 붙잡고 놓아주지 않는다.

3. 사원 1의 업무가 끝나고 보고받고 나서야, 사원2에게 업무 B를 지시한다.

4. [Blocking 방식의 작업 처리] 사원2가 자신의 일이 끝날 때까지 팀장님을 붙잡고 놓아주지 않는다.

```

### 3. Non-blocking + Synchronous

```
1. [비동기적 업무 지시] 팀장님이 사원1, 사원2, 사원3에게 각각 업무 A, B, C를 지시하였다.

2. 그리고 팀장님은 다른 업무를 보기 시작한다. (+ 중간중간 사원에게 업무 다했냐고 질문)

3. [Non blocking 방식의 작업 처리] 사원들은 각자 본인의 맡은 업무를 모두 수행이 끝나는대로 보고한다.
```

### 4. Non-blocking + Asynchronous

```
1. [동기적 업무 지시] 팀장님이 사원1에게 업무 A를 지시하고, 사원1의 업무를 마칠 때까지 모니터 뒤에서 기다린다.

2. [Non blocking 방식의 작업 처리] 사원1이 업무 A를 끝내면 팀장님이 확인한다.

3. [동기적 업무 지시] 팀장님이 사원2에게 업무 B를 지시하고, 사원2의 업무를 마칠 때까지 모니터 뒤에서 기다린다.

4. [Non blocking 방식의 작업 처리] 사원2가 업무 B를 끝내면 팀장님이 확인한다.
```