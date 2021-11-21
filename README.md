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
  

 • argument 는
  
		  1. option:(Verbose mode)
		  2. :option:(Silent mode) 
		  
## - Verbose mode

  • getopts "a:" 는 a 옵션에 콜론(:)을 붙여 인자를 요구케 함 (Verbose mode)
  
  • 옵션은 $opt로 들어간다.
  
  • argument는 $OPTARG로 들어간다.
  
    • Ex) -a "hello world"
  
      • $opt: 'a'
  
      • $OPTARG: "hello world"
      
      
|Verbose mode|Description|
|---|---|
|invalid  옵션 사용 시, "a:bc" 만 허용 하는데, -d 같은 것 넣은 경우|opt 값을 ?문자로 설정하고 OPTARG 값은 unset. 오류 메시지 출력|
|argument 안 넣었을 때, "a:bc"로 설정해 -a 'arg' 넣어야하는데 -a 만 넣은 경우|opt 값을 ?문자로 설정하고 OPTARG 값은 unset. 오류 메시지 출력|


 ## - Silent mode
 
  • getopts " : a : " 는 a 옵션 앞에 콜론(:)을 붙여 더 세밀한 error handling이 가능하게 한다. (Silent mode)
  
  
|Silent mode|Description|
|---|---|
|invalid  옵션 사용 시, "a:bc" 만 허용 하는데, -d 같은 것 넣은 경우|opt 값을 ?문자로 설정하고 OPTARG 값은 해당 옵션 문자로 설정|
|argument 안 넣었을 때, "a:bc"로 설정해 -a 'arg' 넣어야하는데 -a 만 넣은 경우|opt 값을 :문자로 설정하고 OPTARG 값은 해당 옵션 문자로 설정|


#### while getopts " a : hd " opt; do (a옵션은 argument(verbose mode)를 가지고, 나머지 옵션은 그냥 옵션만 가진다)
  
#### while getopts " : a : hd " opt; do (a옵션은 argument(silent mode)를 가지고, 나머지 옵션은 그냥 옵션만 가진다)

