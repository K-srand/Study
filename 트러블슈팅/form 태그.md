1. document.getElementById를 사용하여 id를 얻어와 각각 id, pwd의 value를 비교하여 아이디, 패스워드 입력 여부를 판단하고자 함. 입력 여부는 성공하였으나 파라미터 값이 전달이 되지 않아 submit 시 로그인 실패로 떨어짐. 

2. 개발자 도구의 콘솔창을 확인해보니 "Submit is not a function" 에러가 발생함. 해당 에러에 대해 가장 사례가 비슷한 5~6개의 정보를 추려본 결과 js가 실행되기도 전에 button이 submit을 실행시켜 발생한 에러로 판단됨. 

3. click 이벤트 이후에 submit을 실행해야하는 로직인 경우 form 밖으로 button을 빼는 방법을 추천하여 검증해봄. 그 결과 submit 시 정상적으로 출력되었고 폼에서 값을 전송할 때 누락되었음을 확인할 수 있었음. 

4. 기존 코드 양식을 지키기 위해 form 안에 button을 넣고 실행해보았는데 이전에 실패로 떨어졌던게 성공하기 시작함. 일시적인 오류로 보여 안정성을 위해서 다른 프로젝트를 진행할 때는 form 밖으로 button을 빼는 방법을 사용하도록 해야되겠다고 생각함.

5. 추가로 프로그램 생산성과 가독률을 높이기 위해 id 요소를 얻어오는 방식에서 동적 form을 이용하는 방식으로 수정함.

https://blog.naver.com/akira54055/60035061694 [document.form 사용]
https://www.cikorea.net/bbs/view/etc_qna?idx=17332&lists_style=[폼에서 값을 전송할 때 누락하는 원인]