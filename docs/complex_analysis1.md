
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
```py
import numpy as np
from scipy.integrate import quad
import cmath # Python의 복소수 수학 라이브러리

# 적분할 함수 정의 (z0=0.5, f(z)=z**2)
z0 = 0.5
def f(z):
    return z**2

# 피적분 함수 g(z) = f(z) / (z - z0)
def integrand_func(z):
    return f(z) / (z - z0)

# 경로를 매개변수화하여 실수 적분으로 변환
def integration_path_func(t):
    # z(t) = exp(i*t), dz/dt = i*exp(i*t)
    z_t = cmath.exp(1j * t)
    dz_dt = 1j * cmath.exp(1j * t)
    # 실제 적분할 값: g(z(t)) * dz/dt
    return integrand_func(z_t) * dz_dt

# SciPy의 quad 함수는 실수 함수만 적분할 수 있으므로,
# 실수부와 허수부를 분리하여 각각 적분합니다.
def real_part_integrand(t):
    return np.real(integration_path_func(t))

def imag_part_integrand(t):
    return np.imag(integration_path_func(t))

# 0부터 2*pi까지 적분 수행
integral_real, err_real = quad(real_part_integrand, 0, 2*np.pi)
integral_imag, err_imag = quad(imag_part_integrand, 0, 2*np.pi)

# 최종 적분 결과
contour_integral_result = integral_real + 1j * integral_imag

# 코시 공식 검증: 결과값 / (2*pi*i) 가 f(z0)와 같아야 함
f_z0_calculated = contour_integral_result / (2 * np.pi * 1j)

print(f"수치 적분 결과: {contour_integral_result:.4f}")
print(f"공식에 의한 f(z0) 추정치: {f_z0_calculated:.4f}")
print(f"실제 f(z0) 값 (0.5^2): {f(z0):.4f}")
# 결과가 0.25에 가까워짐을 확인할 수 있습니다.

```

```py
from sympy import symbols, apart, residue, pi, I

z = symbols('z')

# 예시 함수: f(z) = 1 / (z^2 + 1) = 1 / ((z-i)(z+i))
f_z = 1 / (z**2 + 1)

# 특이점 찾기 (분모가 0이 되는 지점)
# 이 경우 특이점은 z = I (i) 와 z = -I (-i) 입니다.

# 특이점 z0 = I 에서의 유수 계산
res_at_I = residue(f_z, z, I)
print(f"z = I 에서의 유수: {res_at_I}") # 결과: -I/2

# 특이점 z0 = -I 에서의 유수 계산
res_at_minus_I = residue(f_z, z, -I)
print(f"z = -I 에서의 유수: {res_at_minus_I}") # 결과: I/2

# 만약 두 특이점을 모두 포함하는 경로를 적분한다면,
# 총 적분값은 2*pi*I * ((-I/2) + (I/2)) = 0 이 됩니다.
total_integral_symbolic = 2 * pi * I * (res_at_I + res_at_minus_I)
print(f"유수 정리에 의한 총 적분값: {total_integral_symbolic}") # 결과: 0


```
