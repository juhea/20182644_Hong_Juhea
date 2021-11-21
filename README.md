# 20182644_Hong_Juhea

---
# ***(쉘 스크립트 관련) getopt 및 getopts 명령어***


- 쉘 스크립트에서 명령을 실행할 때 실행 인자 및 옵션을 필요로 함
- getopt는 사용될 문자열을 입력 받고 다음에는 옵션으로 활용되는 변수를 사용

### - getopt를 사용하는 이유 
  1. 다양한 입력 값이 존재할 경우 사용자와 개발자의 편의를 보장하기 위해서
  2. 스크립트를 보다 체계적으로 관리할 수 있기 때문


### - getopt를 사용할 때 주의할 점
	“ : ” 한 개의 문자만을 구분자로 사용,
 	사용할 문자열 뒤에 ":"을 붙이게 되면 뒤에 value가 붙게 된다.

## - 실행 옵션 예제

- 인자가 있는 실행 옵션

	- 옵션 뒤에 ":"를 붙여줌. 
	- "m", "u"옵션이 해당
		- getopt_test.sh-m test
		- getopt_test.sh-u juhea
 
- 인자가 없는 실행 옵션
 
	- 옵션만 정의
	- "f", "q", "v", "d", "g", "h" 옵션이 해당
		- getopt_test.sh -f -q -v -d -g
		- getopt_test.sh –fqvdg

## - 사용방법 확인

“-h 옵션”을 이용해서 사용법을 확인
	- getopt_test.sh. -h





--------


## 옵션 해석 작업을 쉽게 도와주는 명령이 getopts 이다.


  ![image](https://user-images.githubusercontent.com/94774284/142756801-50eabec8-36c7-4f20-adc7-cf5eb423a6c0.png)
  
   ### while getopts " a : b : h "apt
   
 		 ==> 보통 다음과 같은 형식을 주로 사용
  



