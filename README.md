# 실습 3주차: TypeScript로 기본 계산기 만들기

## 1. 계산기 소개

TypeScript를 사용하여 구현한 간단한 계산기

사칙연산(+,-,×,÷), 소수점 입력, 부호 변경, 퍼센트 계산,
입력 삭제 및 초기화 기능을 제공한다.

계산 로직과 상태 관리, 화면 표시 기능을 분리하여 구현했다.


## 2. 실행 방법

1. 프로젝트 폴더의 터미널에서 다음 명령어 실행.
npm install
npm run build
2. 빌드가 완료되면 TypeScript 파일이 JavaScript로 변환되어 `js` 폴더에 생성됨.
3. index.html 파일을 브라우저에서 열면 계산기가 실행됨.

## 3. 실습 결과

각 테스트를 시작하기 전에 AC를 눌러 계산기를 초기화 한 후 입력하고 그 결과를 확인했다.

1. 기본 계산 확인
모든 계산 예상 결과와 확인 결과가 동일하게 나왔다.
12 → + → 3 → =	15      | `operations.ts` - `add()` 
12 → − → 3 → =	9       | `operations.ts` - `subtract()` 
12 → × → 3 → =	36      | `operations.ts` - `multiply()`
12 → ÷ → 3 → =	4       | `operations.ts` - `divide()`
0.1 → + → 0.2 → =	0.3 | `operations.ts` - `add()`, `calculator.ts` - `formatNumber()`
123 → ⌫	12             | `calculator.ts` - `handleKey()`의 `delete` 처리
5 → +/−	-5              | `calculator.ts` - `handleKey()`의 `sign` 처리
50 → %	0.5             | `calculator.ts` - `handleKey()`의 `percent` 처리 
6110000	6,110,000       | `app.ts` - `formatDisplay()` 

사칙연산은 `operations.ts`에서 처리하고, 삭제·부호 전환·퍼센트 기능은 `calculator.ts`의 `handleKey()`에서 처리하는 것을 확인했다.

2. 계산식과 초기화 확인
`12 → +`를 입력하면 계산식에 `12 +`가 표시되었다.
이후 `3`을 입력하면 `12 + 3`으로 변경되고, `=`을 누르면 계산식에는 `12 + 3 =`, 결과에는 `15`가 표시되는 것을 확인하였다.
계산이 끝난 뒤 숫자 `7`을 입력하면 이전 계산식이 지워지고 새로운 입력 `7`이 시작되었다.
`AC`를 누르면 계산식과 기존 계산 상태가 초기화되고 결과가 `0`으로 돌아가는 것을 확인하였다.
관련 기능은 `calculator.ts`의 `inputDigit()`, `selectOperator()`, `equals()`, `clear()`에서 처리한다.

3. 오류와 복구 확인
`12 → ÷ → 0 → =`을 입력하여 0으로 나누는 경우를 확인하였다.
`operations.ts`의 `divide()`에서 두 번째 숫자가 0인지 검사하고, 0인 경우 오류를 발생시킨다.
오류 처리 과정은 다음과 같다.
`divide()` 오류 발생 → `handleKey()`의 `catch` → `state.error`에 오류 메시지 저장 → `app.ts`의 `render()`에서 화면에 표시
실행 결과 `Error`와 `0으로 나눌 수 없습니다.`라는 메시지가 표시되는 것을 확인하였다.
오류 발생 후 숫자 `7`을 입력하면 오류 상태가 초기화되고 새로운 숫자 `7`이 표시되는 것을 확인하였다.

4. 연속 입력과 작은 화면 확인
모든 연속 입력 예상 결과와 확인 결과가 동일하게 나왔다.
ab으로 버튼에 초점을 옮긴 뒤 Enter 또는 Space로 버튼을 누를 수 있는지도 확인 완료했다.