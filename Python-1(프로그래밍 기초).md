# Python-1 (프로그래밍 기초)



## 1. 프로그래밍 기초 강좌



Top-down 형식으로 문제를 접근해라



* 명령(instruction)

입력을 받아서 출력을 하는 순차적인 집합



#### 디버깅

* **syntax error**

* **runtime error**

* **semantic error**

*소프트웨어 작성할때 전체기간 절반이상을 디버깅 과정에 할애해라*



python 3.8

pillow lib 설치 cmd > py -m pip install Pillow



## 1. 프로그래밍 작성 예제

**함수** : 여러개의 프로그램 명령어를 모아 놓은것

​          새로운 함수의 이름과 함수가 호출될 때 실행될 명령들로 만들어짐

​          실행 순서 : 왼쪽 -> 오른쪽, 위 -> 아래 방향

```python
def print_message():      	# 함수정의, def : 함수정의 키워드
  print("hello, python")
  print("second_lien")
    
def repeat_message():		# 함수정의
  print_message()			# 함수 실행
  print_message()
    
repeat_message()    		# 함수 실행
```



#### 휴보로봇 실습

```python
from cs1robots import *		# lib import
create_world()
hubo=Robot(beepers=1)		# beeper가 1인 Robot을 hubo라고 생성
hubo.move()					# hubo 1칸 이동
hubo.turn_left()			# hubo 왼쪽으로 90도 회전
def turn_right():			# hubo 오른쪽으로 90도 회전하는 함수 정의
    hubo.turn_left()
    hubo.turn_left()
    hubo.turn_left()
turn_right()				# hubo 오른쪽으로 90도 회전
hubo.turn_right()			# 이렇게 실행하면 당연히 안됨! 
                            # turn_right는 현재 쉘에서 정의한 함수이므로 hubo안에 존재X
```

####  

#### ⚡Top-down(하향식 설계)

> 하나의 큰 문제를 중간 크기의 여러 문제로 나누고, 
>
> 중간 크기의 문제 하나 하나를 어떻게 해결할 지 파악합니다.
>
> 그리고, 중간 크기의 문제에 대한 해결책을 작성하기 위해 더 작은 크기의 문제들로 나눕니다. 
>
> 문제가 쉽게 풀수 있을 만큼 작아지면, 작은 문제에 대한 해결책을 작성한 뒤, 그 해결 책들을 모아서 보다 큰 문제에 대한 해결책으로 활용합니다.



#### 휴보의 신문배달(Top-down형식으로 접근)

**문제 개요 **

1. 계단 4칸 올라가기 : climb_up_four_stairs() -

2. 신문 놓기 : hubo.drop_beeper()

3. 돌아서기(180도) : turn_around() -> 왼쪽으로 2번 == 180도 회전

4. 계단 4칸 내려가기 : climb_down_four_stairs()

   

#### ⚡ **Computational Thinking 컴퓨팅사고** 

**쉬운 단계부터 접근**

1. 돌아서기(180도) : 왼쪽으로 2번 돌면 180도 회전

   ```python
   def turn_around():
     hubo.trun_left()
     hubo.trun_left()
   ```

2. 계단 4칸 올라가기 : 계단을 한 칸씩 4번 올라간다.

   -> 계단 한칸씩 * 4번 = climb_up_one_stair()

   ```python
   def climb_up_four_stairs():
     climb_up_one_stair()
     climb_up_one_stair()
     climb_up_one_stair()
     climb_up_one_stair()
       
   def climb_up_one_stair():
     hubo.turn_left()
     hubo.move()
     turn_right()
     hubo.move()
     hubo.move()
   ```

   반복된 코드 제거하기

   ```python
   def climb_up_four_stairs():
     for i in range(4):
       climb_up_one_stair()
   ```

   


