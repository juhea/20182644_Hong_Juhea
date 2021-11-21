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


### - 주의할 점

  • : a : hd
  
     a만 argument를 요구(silent mode)
  
  • h : a : d
  
     의도: a를 argument 요구(silent mode) 하고 싶음
  
     실제 실행: 
  
        h argument 요구(verbose mode) 
	        a argument요구(verbose mode)
    
---


# (리눅스 명령어 관련) sed 및 awk 명령어

---
### sed 명령어

	ed명령어와 grep명령어 기능의 일부를 합친 것이 sed(stream editor)명령어
	
	sed명령어도 grep명령어와 같은 필터이지만 이 명령어는 파일을 수정할 수 있게 하는 반면 ed처럼 대화식처리는 불가능
	
	sed명령어는 1개 라인씩 입력 라인을 읽어들여서 표준출력으로 출력
	
	sed는 각 라인을 읽을 때마다 ed에서 사용하던 형식의 대치작업을 실행
	
	일치하는 문자열이 있으면 그 문자열을 대치한 후 출력하고 일치하는 문자열이 없으면 그 라인은 수정되지 않고 그대로 출력
	
  
#### sed명령어가 ed보다 좋은 점

  - 라인들을 하나씩 읽고, 수정하고, 출력하기 때문에 기억장치 안의 버퍼를 사용하지 않는다는 것
  - 버퍼를 사용하지 않으면 파일의 크기에 제한 없이 작업을 할 수 있음
  - 아주 큰 파일을 처리할 때 주로 사용
  
#### sed 명령어를 호출하는 형식은 grep명령어와 같지만 완전한 형식의 대치 연산자를 사용한다는 점만이 다르다.






