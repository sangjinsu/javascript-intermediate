# Argument 처리 구조

- 파라미터를 `{key, value}` 형태로 저장한다
- 파라미터 수만큼 0부터 인덱스를 부여하여 key로 사용한다
- 파라미터로 받은 값을 value에 설정한다
- `{0: param1, 1: param2}`
- Array-like object => key 값이 0부터 1씩 증가하고 length를 가지고 있다

## 생성 과정

1. 파라미터 값을 넘겨 받는다
2. Argument 오브젝트를 생성하고 parameter 수를 length로 설정한다
3. 0부터 key로 하여 순서대로 파라미터 값을 설정한다
4. 이 과정은 함수 초기화 단계에서 실행한다 

