
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
