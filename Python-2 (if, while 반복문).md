# Python-2 (if, while 반복문)

* 목차

  * 반복문
    * if-else
    * elif
    * while
  * 휴보의 세계일주 예제
  * 좋은 코드 작성원칙

  ---

  

## 2. if 조건문과 while 반복문

#### **if-else문**

```python
if 3 < 5:						# 조건
  print("3 is less than 5")		# 조건이 참이면, 실행
else:
  print("3 is larget than 5")	# 조건이 거짓이면, 실행
```

조금 더 복잡한 if-else문을 살펴보면,

```python
if hubo.on_beeper():
  hubo.pick_beeper()
else:
  if hubo.front_is_clear():
    hubo.move()
  else:
    if hubo.right_is_clear():
      turn_right()
    else:
      turn_around()
```

너무 많은 if,else로 들여쓰기를 한 눈에 파악하기 힘들다.

그래서 자주 사용하는 elif문으로 바꿔보자.

#### **elif문**

else+if를 합친 elif문. 가독성이 훨씬 좋아진것을 알 수 있다.

```python
if hubo.on_beeper():
  hubo.pick_beeper()
elif hubo.front_is_clear():
  hubo.move()
elif hubo.left_is_clear():
  hubo.turn_left()
elif hubo.right_is_clear():
  turn_right()
else:
  turn_around()
```



#### 💡휴보의 80일간의 세계일주

**해결 과정 :**

  ① 시작점에 비퍼를 놓는다

  ② 벽을 만날 때까지 전진한다

  ③ 좌회전한다

  ④ 2, 3번 과정을 비퍼를 발견할 때까지 반복한다

  ⑤ 비퍼를 발견하면 종료한다

**소스 :**

```python
# 직사각형 세계에서만 가능
import time
slepp_time=0.5

hubo.drop_beeper()				# 1번 
hubo.move()						# 1번과정 이후, while문을 실행하기 위해 위치이동
while not hubo.on_beeper():		# 2~3번과정 반복	
  if hubo.front_is_clear():		# 벽을 만나지 않으면, 2번
    time.sleep(sleep_time)
    hubo.move()
  else:							# 벽을 만났다면, 3번
    time.sleep(sleep_time)
    hubo.turn_left()
```

하지만 위의 코드는 직사각형 벽이 있는 경우에만 제대로 실행된다.

![image-20210216165014201](C:\Users\mh\AppData\Roaming\Typora\typora-user-images\image-20210216165014201.png)

위와 같은 코드로 작성하면 `hubo`는  (1,1) (7,1)  (7,3)  (1,3)으로만 돌다가 끝난다...

우회전을 할 수 있는 `hubo`가 필요하다, 그래서 우회전을 할 수 있게 소스를 조금 변형해주면

```python
# 우회전 기능 추가
hubo.drop_beeper()				
hubo.move()						
while not hubo.on_beeper():		
  if hubo.rigth_is_clear():		# 오른쪽 벽이 막혀있지 않은 경우
    turn_right()				# 90도 오른쪽방향으로 회전
    hubo.move()					# 꼭 hubo가 움직이도록 해야한다. 안그러면 무한루프를 만나게됨..
  elif hubo.front_is_clear():		
    time.sleep(sleep_time)
    hubo.move()
  else:							
    time.sleep(sleep_time)
    hubo.turn_left()
```

![image-20210216170015160](C:\Users\mh\AppData\Roaming\Typora\typora-user-images\image-20210216170015160.png) ![image-20210216170105229](C:\Users\mh\AppData\Roaming\Typora\typora-user-images\image-20210216170105229.png)이런 경우 `hubo.move()`가 불가능하다....

```python
# 곤란한 시점에서 빠져나가는 기능 추가
hubo.drop_beeper()				
while not hubo.front_is_clear():	# hubo가 앞이 뚫려 있을때까지 
  hubo.turn_left()  				# 왼쪽으로 회전하여
hubo.move()							# 앞으로 이동한다.

while not hubo.on_beeper():		
  if hubo.rigth_is_clear():		# 오른쪽 벽이 막혀있지 않은 경우
    turn_right()				# 90도 오른쪽방향으로 회전
    hubo.move()					# 꼭 hubo가 움직이도록 해야한다. 안그러면 무한루프를 만나게됨..
  elif hubo.front_is_clear():		
    time.sleep(sleep_time)
    hubo.move()
  else:							
    time.sleep(sleep_time)
    hubo.turn_left()
```



#### :star:사람이 이해하기 좋은 코드 작성원칙:star:

1. 간단하게 시작하기 
2. 한번에 하나의 작은 작업만 수행하기(Refinement:상세화)
3. 각각의 작업들이 이전 작업에 영향 주지 않기
4. 알기쉬운 유용한 주석달기 : # this is comment
5. 의미를 잘 전달하는 이름 고르기



---



### **📃연습문제**

#### Q1

다음 코드의 결괏값은 무엇일까?

```python
a = "Life is too short, you need python"

if "wife" in a: print("wife")
elif "python" in a and "you" not in a: print("python")
elif "shirt" not in a: print("shirt")
elif "need" in a: print("need")
else: print("none")
```

#### A1

​	먼저 참이 되는 조건이 세번째 조건이므로, "shirt"가 출력된다.

---

#### Q2

while문을 사용해 1부터 1000까지의 자연수 중 3의 배수의 합을 구해 보자.



#### A2

```python
result = 0
i = 1
while i <= 1000:
    if i % 3 == 0: # 3으로 나누어 떨어지는 수는 3의 배수
        result += i
    i += 1

print(result) # 166833 출력
```

---

#### Q3

while문을 사용하여 다음과 같이 별(`*`)을 표시하는 프로그램을 작성해 보자.

```
*
**
***
****
*****
```

#### A3

```python
i = 0
while True:
    i += 1 # while문 수행 시 1씩 증가
    if i > 5: break     # i 값이 5보다 크면 while문을 벗어난다.
    print ('*' * i)     # i 값 개수만큼 *를 출력한다.
```



---

#### Q4

for문을 사용해 1부터 100까지의 숫자를 출력해 보자.

#### A4

```python
>>> for i in range(100):
...    print(i+1)
```



----

#### Q5

A 학급에 총 10명의 학생이 있다. 이 학생들의 중간고사 점수는 다음과 같다.

[70, 60, 55, 75, 95, 90, 80, 80, 85, 100]

for문을 사용하여 A 학급의 평균 점수를 구해 보자.

#### A5

```python
A = [70, 60, 55, 75, 95, 90, 80, 80, 85, 100]
total = 0

for score in A:
    total += score   # A학급의 점수를 모두 더한다.

average = total / len(A) # 평균을 구하기 위해 총 점수를 총 학생수로 나눈다.
print(average) # 평균 79.0이 출력된다.
```



---

#### Q6

리스트 중에서 홀수에만 2를 곱하여 저장하는 다음 코드가 있다.

```python
numbers = [1, 2, 3, 4, 5]
result = []
for n in numbers:
    if n % 2 == 1:
        result.append(n*2)
```

위 코드를 리스트 내포(list comprehension)를 사용하여 표현해 보자.

#### A6

```python
numbers = [1, 2, 3, 4, 5]
result = [n*2 for n in numbers if n%2==1]
print(result)		# [2, 6, 10]
```

