# 20182644_Hong_Juhea

---
# ***(쉘 스크립트 관련) getopt 및 getopts 명령어***

---

## ***getopt 명령어***

---

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


## ***getopt 명령어***


----


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


# ***(리눅스 명령어 관련) sed 및 awk 명령어***

---

## ***sed 명령어***

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


# sed 명령어 사용법


#### # 치환(substitute)
---------

			sed 's/addrass/address/' list.txt  
			
				addrass를 address로 바꾼다. 
  
				단, 원본파일을 바꾸지 않고 표준출력만 한다.
  
 			sed 's/\t/\ /' list.txt 
			
				 탭 문자를 엔터로 변환
   
   
#### # 삭제(delete)
------------

			sed '/TD/d' 1.html 
	 			TD 문자가 포함된 줄을 삭제하여 출력한다.
   
   
			sed '/Src/!d' 1.html 
				 Src 문자가 있는 줄만 지우지 않는다.
   
   
			sed '1,2d' 1.html 
				 처음 1줄, 2줄을 지운다.
   
   
			sed '/^$/d 1.html **(중요)**
				 공백라인을 삭제하는 명령이다.
   
---
 
      
### sed 명령어의 다양한 사용예제
------

	1. 특정문자열 바꾸기
	
	2. 특정문자열이 포함된 행 삭제하기
	
 	3. 특정 문자열이 포함된 행에서 특정문자만 삭제하기
	
	4. 파일의 일부만 편집해야 할 경우 라인의 범위를 지정하여 사용 가능
	
	5. 라인 번호 대신 문맥을 범위로 지정한 경우
	
 	6. 세번째 라인을 삭제
	
	7. hello 문자가 들어있는 line만 프린트
	
-------

### /^$/   

	공백라인, 즉 라인의 시작과 끝 사이에 아무것도 없는 라인과 부합한다. 
  
	이것은 공백 스페이스들로 된 라인과는 부합하지 않는바, 스페이스 자체가 문자이기 때문이다.
	
---

  
###  sed '/^ *$/d’

	--> space로 만들어진 공백까지 제거 
	
                       (^와 *사이에 공백이 있어야 한다)
                       
---

### sed 명령어의 또 다른 기능

		sed명령어의 –f(file) 선택자를 사용하면 명령어를 일일이 키보드에서 입력하지 않고
		
		하나의 파일에 기억시켜 놓고 사용할 수도 있다.
		
   			 # sed -f command.file in.file
			 
 		여러 개의 명령어를 연속적으로 자주 사용할 때 이 명령어 파일이 유용하게 사용된다.
		
		
		예를 들어 다음과 같은 복수 개의 명령어가 파일에 기억되어 있는 경우는
		
     			  # vi command.file
       
      			 s/hello/goodbye
       
     			 s/good/bad
     
    다음과 같은 명령어를 입력하면 다음과 같이 출력된다.
  
     	 # echo "1234hello5678" | sed -f command.file       
      
      
          => 1234badbye5678
---


## ***awk 명령어***

        데이터 처리를 위한 유닉스 프로그래밍 언어
	
        구버전은 awk, 새로운 버전은 nawk, GNU 버전은 gawk 라는 명령어로 사용
	
---

#### awk 기본 사용법

     패턴과 command로 이루어짐
  
 	 패턴 부분
  
  	   - 정규식이나 조건 표현식(true/false)이 올 수 있음
     
    	  1. 정규식 
      		   Ex) /^hello$/ 
  
      	  2. 조건 표현식 
     		    Ex) $1 >= 0
      	
	  command 부분
  
    		  - c언어와 마찬가지로 조건연산자, 반복연산자, 산술연산자, 논리연산자, 
		  		삼항연산자, 증감연산자, 대입연산자 등을 사용 가능
       
       
     		  - 아무 command를 지정하지 않을 경우, 패턴에 매칭된 줄을 그대로 출력하는 기본 동작을 수행
   
   
   		  - command 부분은 { }로 감싼다
		  
         		  Ex) { if($1 >= 0){ print "hello"; } }
			  
----			  
			  
     * 정규표현식    
      
        - 정규표현식을 사용할 때는 슬래시 /로 감싼다  
        
        - grep, sed와 마찬가지로 정규표현식 메타문자를 사용
        
       		   ※  단 단어 지시자 \<\>, 캡처 \(\), 반복 지시자 \{\}는 사용할 수 없음
	  
---

### Field Separatorawk
      
            필드 구분자를 기준으로 각 줄의 필드를 나누어 처리 
      
            필드 구분자는 FS라는 이름의 내장변수로 관리되며 기본값은 탭/스페이스


---

### awk 구조

| 시작 (Begin) | 시작 단계로서 전체 스크립트를 위한 정의 단계 (Preprocessor)|
|:---:|:---:|
| 실행 (Routin) | 실행단계로 이 스크립트의 기능을 수행하는 단계 |
| 끝 (End) | 마무리 단계로 결과 출력 단계|

---


### awk 옵션
      
        -  F 옵션
        $ awk -F: {print $1} file    
        
                  # 콜론(:) 을 필드 구분자로 사용
                  
                  
        $ awk -F'[:,]' {print $1} file    
        
                  # 콜론(:)과 콤마(,)를 필드 구분자로 사용-F 옵션을 사용하여 필드 구분자를 직접 지정할 수도 있음
                  
                  
![image](https://user-images.githubusercontent.com/94774284/142760342-a6ec41a8-08e2-400c-a443-e084e7a2a300.png)
                  
----


### awk 의 사용


          일반적으로 grep 과 같이 사용
          
    
              1. grep 을 이용하여 데이터 파일의 구조 확인  
              
              2. 정규화가 가능하지를 확인하고 sed로 테스트 한후에 awk 가 처리할수 있을정도로
              
                 정규화되있다면 awk를 사용 
              
              3. sed로 정규화된 양식을 awk 로 처리
              
              
---

### awk 시스템 변수

| 변수 | 내용|
|:---:|:---:|
| $0 | 입력 라인 모두 |
| $n | 입력 라인에서 n번째 필드 값|
| ARGC | 명령 라인 인자 수를 갖는 변수|
| ARGV | 명령 라인의 인자를 포함하는 배열 |
| ENVIRON | 환경 변수들을 모아둔 관계형 배열 |
| FILENAME | 현재 파일명 |
| FS | 구분자 정의, 공백을 기본으로 사용 |
| FNR | 입력 파일의 레코드 총수 (라인 수) |
| NF | 현재 레코드 필드 수 |
| OFMT | 숫자에 대한 출력 포맷 |
| OFS | 출력 필드 구분, 빈 라인을 기본으로 사용 |
| ORS | 출력 레코드 구분 (newline을 기본으로 사용) |
| RLENGTH | 지정한 패턴으로 검색되어 나온 문자열의 길이 |
| RS | 입력 레코드 구분 (newline을 기본으로 사용) |
| RSTART | 지정한 패턴으로 검색되어 나온 문자열의 가장 앞부분 |


---


### awk 명령어

| 명령어 | 내용|
|:---:|:--------------:|
| awk '/west/' datafile | west 라는 글이 있는 줄 출력 |
| awk '/^north/' datafile | north로 시작하는 줄 출력 |
| awk '/^(no | so)/' datafile | no 또는 so 로 시작하는 줄 출력 |
| awk '{ print $3, $2 }' datafile | datafile 리스트의 세 번째 와 두 번째 필드를 스페이스로 띄어서 출력 |
| awk '{ print $3 $2 }' datafile | datafile 리스트의 세 번째 와 두 번째 필드를 그냥 붙여서 출력 |
| awk '{ print "Number of fields : " NF} ' datafile | datafile의 각 줄마다의 필드수를 리턴|
| awk '$5 ~ /\.[7-9]+/' datafile | 다섯 번째 필드가 마침표 다음엣 7과 9사이 숫자가 하나 이상 나오는 레코드 출력 |
| awk '$2 !~ /E/ { print $1, $2 }' datafile | 두 번째 필드에 E 패턴이 없는 레코드의 첫 번째와 두 번째 필드 출력 |
| awk '$3 ~ /^Joel/{ print $3 " is a nice guy."} ' datafile | 세 번째 필드가 Joel로 시작하면 " is a nice guy"와 함께 출력|
| awk '$8 ~ /[0-9][0-9]$/ { print $8 }' datafile | 여덟 번째 필드가 두 개의 숫자이면 그 필드가 출력
| awk '$4 ~ /Chin$/ { print "The price is $" $8 "." }' datafile | 네 번째 필드가 Chine으로 끝나면 "The price is $" 8번 필드 및 마침표가 출력|
| awk -F: '{ print $1 } ' datafile | -F 옵션은 입력 필드를 ':'로 구별 |
| awk -F"[ :]" '{ print $1, $2 } ' datafile | 입력 필드로 스페이스와 ':'를 필드 구별자로 사용 |
| awk -f awk_script.file datafile | -f 옵션은 awk 스크립트 파일 사용할 때 씀 |
| awk '$7 == 5' datafile | 7번 필드가 5와 같다면 출력|
| awk '$2 == "CT" { print $1, $2 }' datafile | 2번 필드가 "CT" 문자와 같으면 1, 2 번 필드 출력 |
| awk '$7 <5 { print $4, $7}' datafile | 7번 필드가 5보다 작다면 4번, 7번 필드 출력 |
| awk '$6 >.9 { print $1, $6}' datafile | 6번 필드가 .9 보다 크다면 1번, 6번 출력 |
      
      
---      







#### 										감사합니다




