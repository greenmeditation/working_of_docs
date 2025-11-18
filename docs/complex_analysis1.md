
# Complex Analysis

```py
	복소수 생성	z = 2 + 3j or z = complex(2, 3)
실수부/허수부 접근	z.real, z.imag
절대값 (크기)	abs(z)
켤레 복소수	z.conjugate()
NumPy	복소수 배열 생성	arr = np.array([1+2j, 3-4j])
기본 연산 (배열)	arr * 2, arr + arr (배열 연산 지원)
from sympy import *
z = symbols('z')

x, y = symbols('x y', real=True)
expr = x + I*y

solve(z**4 - 1, z)

limit(sin(z)/z, z, 0)

diff(f(z), z)


integrate(f(z), z)


Series(f(z), z, z0, n)


re(expr), im(expr)


polar_lift(z)

pi, e, inf 상수	np.pi, np.e, np.inf
복소 함수 (배열 지원)	np.exp(arr), np.log(arr), np.sin(arr)
위상각 (편각)	np.angle(arr) (라디안 값 반환)
극좌표 변환	np.abs(arr), np.angle(arr)
SciPy	특수 함수	scipy.special.gamma(z) 등
수치 적분	scipy.integrate.quad(func, a, b)


```

```py
from sympy import symbols, integrate, pi, I

# 변수 및 함수 정의
z, z0 = symbols('z z0')
f_z = z**2 # 예시 함수 f(z) = z^2 (전 해석 함수)

# 코시 공식의 피적분 함수
integrand = f_z / (z - z0)

# SymPy는 기본적으로 경로를 지정하기보다 일반적인 적분 함수를 제공합니다.
# 경로 적분을 직접 심볼릭하게 계산하는 것은 복잡하며, 보통 수치적으로 접근합니다.
# SymPy는 특이점 주변의 적분 개념보다는 유수 정리에 더 가깝게 동작합니다.

```
