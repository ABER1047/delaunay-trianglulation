# delaunay-trianglulation

### 들로네의 삼각분할 (delaunay trianglulation)

해당 프로젝트는 게임메이커로 제작되었지만, 주요 코드는 C위주로만 작성해서 

나중에 100% C로만 다시 리메이크 예정

#

### 들로네의 삼각분할이란?
-------------

들로네 삼각분할은 평면위의 점들을 삼각형으로 연결하여 공간을 분할할 때, 

이 삼각형들의 내각의 최소값이 최대가 되도록 하는 분할을 말한다.

#### ▼ 들로네의 삼각분할의 실제 활용도 및 여러 자세한 내용은 아래 내용 참고

https://darkpgmr.tistory.com/96

#

### ▼ 참고 사항
-------------

코드 내용 설명은 주석이 달려있지만, 대략적인 알고리즘을 보길 권장 (아래 참고)

[주요 계산식 코드]

https://github.com/ABER1047/delaunay-trianglulation/blob/main/scripts/get_triangle/get_triangle.gml

#

### ▼ 미리보기

![preview_1](imgs/preview_1.gif)

#

### ▼ 대략적인 알고리즘 :
-------------

```
들로네의 삼각형의 조건을 컴퓨터 알고리즘화 시키기 위해, 먼저 좌표평면 위 특정한 삼각형에서의 외심을 구해야 하는데 이때, 각 꼭짓점을 A, B, C라고 하였을때, 
A(x1,y2), B(x2,y2), C(x3,y3)라고 하였을때, 3개의 변의 길이는 각각 L1, L2, L3라 하고 
L1 = √[(x2 - x1)2 + (y2 - y1)2] … (이하 생락) 일때, 

삼각형의 외심의 좌표는 각 점들에서의 거리가 모두 같은 곳에 존재하므로, L1 = L2 = L3를 성립해야 한다. 

루트를 제거하기 위해 해당 방정식을 조금 변형한 식인 L12 = L22 = L32를 이용해 해당 방정식을 서로 연립하여 외심의 좌표를 구하게 되면, 

외심 D의 좌표는 D(X,Y)

이때 X는 [(x1 sin 2A + x2 sin 2B + x3 sin 2C)/ (sin 2A + sin 2B + sin 2C)] 
이때 Y는 [(y1 sin 2A + y2 sin 2B + y3 sin 2C)/ (sin 2A + sin 2B + sin 2C)] 이다.

들로네 삼각분할 법칙에 의해, 각 꼭짓점을 이어 만든 삼각형의 외심 내부에는 어떠한 점도 존재하면 안되므로,
특정 삼각형의 외심의 좌표 D(X,Y)와 각 점들의 좌표 P(X,Y)의 거릿값이 외접원의 반지름보다 커야한다.

이때 sin 2A ...들의 값은 sinA와 cosA값을 이전에 이미 구했음으로 이를 이용하면, 

sin2A = sin(A + A) = sinA x cosA + cosA x sinA = 2(sinA*cosB)
(나머지 sin2B, sin2C도 같은 방식으로 구할수 있다.)

이때의 외접원의 반지름을 구하기 위해, 코사인 법칙을 이용해, 

cos(A) = (L3^2 + L1^2 - L2^2)/(2 x L3 x L1)을 구할수 있고, 

이때 사인법칙을 사용하기 위해, [cos(A)^2 + sin(A)^2 = 1] 임을 변형해, 

sin(A) = √[1 - cos(A)^2]임을 구할 수 있으며, 

sin(A)/L2 = 2R (이때 R은 외접원의 반지름)을 통해 특정 삼각형의 외접원의 반지름을 구할 수 있다.

이후, 좌표 평면위에 있는 랜덤한 3개의 점들을 서로 연결하여 삼각형을 만든 뒤, 
이때의 외접원의 반지름의 길이와, 각 점들의 좌표를 통해 구한 외심으로부터, 각 점들까지의 거리를 비교해, 
만약 해당 삼각형의 외심원이 현재 연결된 삼각형의 점이 아닌 모든 다른점으로부터의 거리 값이 외접원의 반지름 보다 크면 해당 삼각형을 유지하고, 
아닌 경우, 해당 삼각형을 지우고, 위와 같은 과정을 더 이상 만들 수 있는 새로운 삼각형의 경우가 없을때까지 반복
```

#

- 2022-07-23 추가 

일부 3개 이상의 점이 극히 작은 소수점 단위의 차이로 

거의 비슷하게 한 직선 위에 있을경우 선이 이상하게 이어지는 경우가 있음.
