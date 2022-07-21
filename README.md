# delaunay-trianglulation

- 들로네의 삼각분할 (delaunay trianglulation)

===================================================================

- 들로네의 삼각분할이란?

특정한 n개의 점이 평면위에 존재할 때(이때 n > 2), 
해당 점들을 모두 이어 삼각형들로만 이루어지게 쪼갤 때(삼각분할)을 할 때, 
각 삼각형의 외접원의 내부에 어떠한 점도 존재하지 않는 경우에서의 삼각분할

===================================================================

- 알고리즘 :

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

이때의 외접원의 반지름을 구하기 위해, 코사인 법칙을 이용해, cos(A) = (L3^2 + L1^2 - L2^2)/(2 x L3 x L1)을 구할수 있고, 
이때 사인법칙을 사용하기 위해, [cos(A)^2 + sin(A)^2 = 1] 임을 변형해, 
sin(A) = √[1 - cos(A)^2]임을 구할 수 있으며, 
sin(A)/L2 = 2R (이때 R은 외접원의 반지름)을 통해 특정 삼각형의 외접원의 반지름을 구할 수 있다.

이후, 좌표 평면위에 있는 랜덤한 3개의 점들을 서로 연결하여 삼각형을 만든 뒤, 
이때의 외접원의 반지름의 길이와, 각 점들의 좌표를 통해 구한 외심으로부터, 각 점들까지의 거리를 비교해, 
만약 해당 삼각형의 외심원이 현재 연결된 삼각형의 점이 아닌 모든 다른점으로부터의 거리 값이 외접원의 반지름 보다 크면 해당 삼각형을 유지하고, 
아닌 경우, 해당 삼각형을 지우고, 위와 같은 과정을 더 이상 만들 수 있는 새로운 삼각형의 경우가 없을때까지 반복
