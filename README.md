# Ordinary Differential Equation<br>

**개요**<br>
* First Order ODE solutions
  * [1. Euler's Explicit]()<br>
  * [2. Euler's Implicit]()<br>
  * [3. Modified Euler's method]()<br>
  * [4. Runge_Kutta 2nd order method]()<br>
  * [5. Runge_Kutta 3rd order method]()<br>
  * [6. Runge_Kutta 4th order method]()<br>
  * [7. Adam-Bashforth method]()<br>
* Second Order ODE solutions
  * [1. Runge_Kutta 2nd order method]()<br>

<hr>

## 1. eulerExplicit( )<br>
```c
void eulerExplicit(double myfunc(const double t, const double y), double t0, double tf, double h, double y0);
```
>Parameter<br>
**myfunc** : 구하고자 하는 함수  <br>
**t0** : 처음 x값 <br>
**tf** : 다음 x값 <br>
**h** : tf-t0<br>
**y0** : y 초기값 <br>
<br>
<hr>

1. 함수 y(x)의 값을 주어진 초기값 y(t0) 부터 기울기 정보를 이용하여 구하는 함수
2. myNP.h 안에 선언되어 있다.<br>
3. Explicit method와 Implicit Method로 나뉜다.
4. 다음과 같은 원리를 기반으로 작성되었다.<br>
   


* **Based on numerical integration**
$$dy=f(x,y)dx$$
$$\int_{y_{i}}^{y_{i+1}}dy=\int_{x_{i}}^{x_{i+1}}f(x,y)dy$$
$$y_{i+1}=y_i+f(x_i,y_i)\cdot(x_{i+1}-x_i)$$
<br>

* **Based on Taylor Series**
$$y(x_{i+1})\approx y(x_i)+y^{'}(x_i)(h)$$
<br>

* **Explicit method**
$$y_{i+1}^{N}=y_i^N+f(x_i,y_i)\cdot h$$
$$x_{i+1}=x_i+h$$

<hr>

### Example <br>
```c++
double myfunc(const double t, const double y);

int main()
{
    double t0 = 0;
    double tf = 0.1;
    double h = 0.01;
    double y0 = 0;

    eulerExplicit(myfunc, t0, tf, h, y0);
}

double myfunc(const double t, const double y)
{	
	double dy = 0;
	dy = -y + cos(2 * PI * 10 * t);
	return dy;
}
```
<hr>

### Output <br>
```c
y[0] = 0.000000
y[1] = 0.010000
y[2] = 0.017990
y[3] = 0.020900
y[4] = 0.017601
y[5] = 0.009335
y[6] = -0.000758
y[7] = -0.008841
y[8] = -0.011843
y[9] = -0.008634
y[10] = -0.000458
```
<hr>

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<br>
<hr>

## 2. eulerImplicit( )<br>
```c
void eulerExplicit(double myfunc(const double t, const double y), double t0, double tf, double h, double y0);
```


>Parameter<br>
**myfunc** : 구하고자 하는 함수  <br>
**t0** : 처음 x값 <br>
**tf** : 다음 x값 <br>
**h** : tf-t0<br>
**y0** : y 초기값 <br>
<br>

1. 함수 y(x)의 값을 주어진 초기값 y(t0) 부터 기울기 정보를 이용하여 구하는 함수
2. myNP.h 안에 선언되어 있다.<br>
3. Explicit method와 Implicit Method로 나뉜다.
4. 다음과 같은 원리를 기반으로 작성되었다.<br>
   


* **Based on numerical integration**
$$dy=f(x,y)dx$$
$$\int_{y_{i}}^{y_{i+1}}dy=\int_{x_{i}}^{x_{i+1}}f(x,y)dy$$
$$y_{i+1}=y_i+f(x_i,y_i)\cdot(x_{i+1}-x_i)$$
<br>

* **Based on Taylor Series**
$$y(x_{i+1})\approx y(x_i)+y^{'}(x_i)(h)$$
<br>



* **Implicit method**
$$y_{i+1}^{N}=y_i^N+f(x_{i+1},y_{i+1})\cdot h$$
$$x_{i+1}=x_i+h$$
<hr>

## Example <br>
```c++
double myfunc(const double t, const double y);

int main()
{
    double t0 = 0;
    double tf = 0.1;
    double h = 0.01;
    double y0 = 0;

    eulerImplicit(myfunc, t0, tf, h, y0);
}

double myfunc(const double t, const double y)
{	
	double dy = 0;
	dy = -y + cos(2 * PI * 10 * t);
	return dy;
}
```

## Output <br>
```c
y[0] = 0.000000
y[1] = 0.007990
y[2] = 0.015980
y[3] = 0.023971
y[4] = 0.031961
y[5] = 0.039951
y[6] = 0.047941
y[7] = 0.055931
y[8] = 0.063921
y[9] = 0.071912
y[10] = 0.079902
```

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<br>

## 3. modifiedEuler( )<br>
```c
double modifiedEuler(double myfunc(const double t, const double y), double t0, double tf, double h, double y0);
```


>Parameter<br>
**myfunc** : 구하고자 하는 함수  <br>
**t0** : 처음 x값 <br>
**tf** : 다음 x값 <br>
**h** : tf-t0<br>
**y0** : y 초기값 <br>
<br>

1. 함수 y(x)의 값을 주어진 초기값 y(t0) 부터 기울기 정보를 이용하여 구하는 함수
2. myNP.h 안에 선언되어 있다.<br>
3. 다음과 같은 원리를 기반으로 작성되었다.<br>
   


**Process**<br>
* Calculate
$${dy\over dx\vert}_{x=x_i} =f(x_i,y_i)$$
$${dt\over dx\vert}_{x=x_i, y=y_i}=f(x_{i+1},y_{i+1}^E)$$

$$where \\y_{i+1}^E=y_i+f(x_i,y_i)\cdot h$$

<br>

* Take acerage slope and get
$$ y_{i+1}=y_i+{{f(x_i,y_i^N)+f(x_{i+1},y_{i+1}^E)}\over 2 }\cdot h$$
$$x_{i+1}=x_i+h$$



## Example <br>
```c++
double myfunc(const double t, const double y);

int main()
{
    double t0 = 0;
    double tf = 0.1;
    double h = 0.01;
    double y0 = 0;

    modifiedEuler(myfunc, t0, tf, h, y0);
}

double myfunc(const double t, const double y)
{	
	double dy = 0;
	dy = -y + cos(2 * PI * 10 * t);
	return dy;
}
```

## Output <br>
```c
y[0] = 0.000000
y[1] = 0.008995
y[2] = 0.014455
y[3] = 0.014296
y[4] = 0.008579
y[5] = -0.000511
y[6] = -0.009501
y[7] = -0.014956
y[8] = -0.014792
y[9] = -0.009070
y[10] = 0.000025
```

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<hr>
<br>

## 4. odeRK2( )<br>
```c
void odeRK2(double myfunc(const double t, const double y), double y[], double t0, double tf, double h, double y0);
```


>Parameter<br>
**myfunc** : 구하고자 하는 함수  <br>
**y[ ]** : y값을 저장하기 위한 배열 선언 <br>
**t0** : x 초기값 <br>
**tf** : x 최종값 <br>
**h**  : x_(i+1) - x_(i)<br>
**y0** : y 초기값 <br>
<br>

1. 기울기는 여러 지점에서의 기울기의 합으로 얻어진다.
2. myNP.h 안에 선언되어 있다.<br>
3. 다음과 같은 원리를 기반으로 작성되었다.<br>
   


$$y_{i+1}=y_i+(C_1K_1+C_2K_2)\cdot h$$
$$K_1=f(t,y)\\ K_2=f(t+\alpha h, y+\beta K_1h)=f(t+\alpha h,y+\beta f(t,y)h)$$

<hr>

$$C_1=C_2={1\over 2}, \alpha=\beta=1$$
$$ y_{i+1}=y_i+{1\over 2}(K_1+K_2)\cdot h $$
$$x_{i+1}=x_i+h$$




## Example <br>
```c++
double myfunc(const double t, const double y);

int main()
{
    double t0 = 0;
    double tf = 0.1;
    double h = 0.01;
    double y0 = 0;

    double y[1000] = { 0 };

    odeRK2(myfunc, y, t0, tf, h, y0);
}

double myfunc(const double t, const double y)
{	
	double dy = 0;
	dy = -y + cos(2 * PI * 10 * t);
	return dy;
}
```

## Output <br>
```c
y[0] = 0.000000
y[1] = 0.008995
y[2] = 0.014455
y[3] = 0.014296
y[4] = 0.008579
y[5] = -0.000511
y[6] = -0.009501
y[7] = -0.014956
y[8] = -0.014792
y[9] = -0.009070
y[10] = 0.000025
```

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<br>

## 5. odeRK3( )<br>
```c
void odeRK2(double myfunc(const double t, const double y), double y[], double t0, double tf, double h, double y0);
```


>Parameter<br>
**myfunc** : 구하고자 하는 함수  <br>
**y[ ]** : y값을 저장하기 위한 배열 선언 <br>
**t0** : x 초기값 <br>
**tf** : x 최종값 <br>
**h**  : x_(i+1) - x_(i)<br>
**y0** : y 초기값 <br>
<br>

1. 기울기는 여러 지점에서의 기울기의 합으로 얻어진다.
2. myNP.h 안에 선언되어 있다.<br>
3. 다음과 같은 원리를 기반으로 작성되었다.<br>
   


$$y_{i+1}=y_i+(C_1K_1+C_2K_2+C_3K_3)\cdot h$$

$$K_1=f(t,y_i)
\\K_2=f(t+\alpha_2 h,y_i+\beta_{21}K_1h)
\\K_3=f(t_i+\alpha_3 h, y_i+\beta_{31}K_1h+\beta_{32}K_2h)$$

* Case 1 : classical third-order Runge-Kutta
$$C_1={1\over 6}, C_2={4\over 6}, C_3={1\over 6}/ \alpha_2={1\over 2}, \alpha_3=1/ \beta_{21}={1\over 2}, \beta_{31}=-1, \beta_{32}=2$$
$$y_{i+1}=y_i+{1\over 6}(K_1+4K_2+K_3)\cdot h$$
$$x_{i+1}=x_i+h$$



## Example <br>
```c++
double myfunc(const double t, const double y);

int main()
{
    double t0 = 0;
    double tf = 0.1;
    double h = 0.01;
    double y0 = 0;

    double y[1000] = { 0 };

    odeRK3(myfunc, y, t0, tf, h, y0);
}

double myfunc(const double t, const double y)
{	
	double dy = 0;
	dy = -y + cos(2 * PI * 10 * t);
	return dy;
}
```

## Output <br>
```c
y[0] = 0.000000
y[1] = 0.009307
y[2] = 0.014964
y[3] = 0.014810
y[4] = 0.008905
y[5] = -0.000494
y[6] = -0.009796
y[7] = -0.015448
y[8] = -0.015289
y[9] = -0.009380
y[10] = 0.000024
```

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<br>

## 6. odeRK4( )<br>
```c
void odeRK2(double myfunc(const double t, const double y), double y[], double t0, double tf, double h, double y0);
```


>Parameter<br>
**myfunc** : 구하고자 하는 함수  <br>
**y[ ]** : y값을 저장하기 위한 배열 선언 <br>
**t0** : x 초기값 <br>
**tf** : x 최종값 <br>
**h**  : x_(i+1) - x_(i)<br>
**y0** : y 초기값 <br>
<br>

1. 기울기는 여러 지점에서의 기울기의 합으로 얻어진다.
2. myNP.h 안에 선언되어 있다.<br>
3. 다음과 같은 원리를 기반으로 작성되었다.<br>
   


$$y_{i+1}=y_i+(C_1K_1+C_2K_2+C_3K_3+C_4K_4)\cdot h$$

$$K_1=f(t,y_i)
\\K_2=f(t+\alpha_2 h,y_i+\beta_{21}K_1h)
\\K_3=f(t_i+\alpha_3 h, y_i+\beta_{31}K_1h+\beta_{32}K_2h)
\\K_4=f(t_i+\alpha_4 h, y_i+\beta_{41}K_1h+\beta_{42}K_2h+\beta_{43}K_3h)$$

* Case 1 : classical Fourth-order Runge-Kutta
$$C_1=C_4={1\over 6}/ C_2=C_3={2\over 6}\\\alpha_2=\alpha_3=\beta_{21}=\beta_{32}={1\over 2}\\ \alpha_4=\beta_{43}=1\\\beta_{31}=\beta_{42}=\beta_{42}=0$$
$$y_{i+1}=y_i+{1\over 6}(K_1+2K_2+2K_3+K_4)\cdot h$$
$$x_{i+1}=x_i+h$$



## Example <br>
```c++
double myfunc(const double t, const double y);

int main()
{
    double t0 = 0;
    double tf = 0.1;
    double h = 0.01;
    double y0 = 0;

    double y[1000] = { 0 };

    odeRK4(myfunc, y, t0, tf, h, y0);
}

double myfunc(const double t, const double y)
{	
	double dy = 0;
	dy = -y + cos(2 * PI * 10 * t);
	return dy;
}
```

## Output <br>
```c
y[0] = 0.000000
y[1] = 0.009307
y[2] = 0.014964
y[3] = 0.014810
y[4] = 0.008905
y[5] = -0.000494
y[6] = -0.009796
y[7] = -0.015448
y[8] = -0.015289
y[9] = -0.009380
y[10] = 0.000024
```

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<br>

## 7. adamBashforth2nd( )<br>
```c
void adamBashforth2nd(double myfunc(const double t, const double y), double t0, double y0, double t1, double y1, double h, double y[], double tf);
```


>Parameter<br>
**myfunc** : 구하고자 하는 함수  <br>
**y[ ]** : y값을 저장하기 위한 배열 선언 <br>
**t0** : 첫번째 x 값 <br>
**t1** : 두번째 x 값 <br>
**y0** : 첫번째 y 값 <br>
**y1** : 두번째 y 값 <br>
**tf** : x 최종값 <br>
**h**  : x_(i) - x_(i-1)<br>
<br>

1. Use two points<br>
$$( x_i,y_i ), (x_{i-1},y_{i-1})$$
2. myNP.h 안에 선언되어 있다.<br>
3. 다음과 같은 원리를 기반으로 작성되었다.<br>
   

    * 2nd order Adam-Bashforth method uses two points 
$$y_{i+1}=y_i+{h\over2}[3f(x_i,y_i)-f(x_{i-1},y_{i-1})] $$



## Example <br>
```c++
double myfunc(const double t, const double y);

int main()
{
    double y_a[1000] = { 0 };
    double t0 = 0;
    double tf = 0.1;
    double y0 = 0;
    double t1 = 0.001;
    double y1 = 0.000999;
    double h = t1 - t0;

    adamBashforth(myfunc, t0, y0, t1, y1, h, y_a, tf);
}

double myfunc(const double t, const double y)
{	
	double dy = 0;
	dy = -y + cos(2 * PI * 10 * t);
	return dy;
}
```

## Output <br>
```c
y[0] = 0.000000
y[1] = 0.009321
y[2] = 0.016316
y[3] = 0.016708
y[4] = 0.010359
y[5] = -0.000303
y[6] = -0.011202
y[7] = -0.018170
y[8] = -0.018544
y[9] = -0.012176
y[10] = -0.001496
```

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<br>

## 1. sysRK2( )<br>
```c
void sysRK2(void func(const double t, const double Y[], double dYdt[]), double K1[], double K2[], double t0, double tf, double h, double y1_init, double y2_init);
```


>Parameter<br>
**func** : y'과 y''을 배열에 저장해 주는 함수  <br>
**K1[ ]** : 크기 2의 K1을 저장하는 배열 <br>
**K2[ ]** : 크기 2의 K2를 저장하는 배열
**t0** : x 초기값 <br>
**tf** : x 최종값 <br>
**y1_init** : y 초기값<br>
**y2_init** : y' 초기값 <br>
**h**  : x_(i) - x_(i-1)<br>
<br>

1. 2nd order Ordinary Differential Equation이다.<br>

2. myNP.h 안에 선언되어 있다.<br>
3. 다음과 같은 원리를 기반으로 작성되었다.<br>
   
* Runge_Kutta to solve 
$$\ddot{y}+c\dot{y}+ky=u(t)$$
<br>

$$z=f_1(t,y,z)={dy\over dt}=\dot{y}$$
$${dz\over dt}=f_2(t,y,z)=-ky-cz+u(t)$$
* Repeat i=1 to n
  $$K_{y1}=f_1(x_i,y_i,z_i)=\dot{y_i}=z_i$$
  $$K_{z1}=f_2(x_i,y_i,z_i)=-ky_i-cz_i+u(t_i)$$
<br>

$$y_{i+1}^E=y_i+K_{y1}h$$
$$y_{i+1}^E=y_i+K_{z1}h$$
<br>

$$K_{y2}=f_1(x_i+h,y_{i+1}^E,z_{i+1}^E)=\dot{y}$$
  $$K_{z1}=f_2(x_i+h,y_{i+1}^E,z_{i+1}^E)=-ky_{i+1}-cz_{i+1}+u(t_i+h)$$
<br>

$$y_{1,i+1}=y_{1,i}+{1\over 2}(K_{y1}+K_{z1})\cdot h$$
$$y_{2,i+1}=y_{1,i}+{1\over 2}(K_{y2}+K_{z2})\cdot h$$






## Example <br>
```c++
void func(const double t, const double Y[], double dYdt[]);

int main()
{
	double K1[2];
	double K2[2];

	double t0 = 0.0;
	double tf = 1.0;
	double h = 0.01;
	double y1_init = 0.0; // Initial value of y
	double y2_init = 0.2; // Initial value of dy/dt

	sysRK2(func, K1, K2, t0, tf, h, y1_init, y2_init);

	return 0;
}

void func(const double t, const double Y[], double dYdt[])
{
	double m = 1;
	double c = 7;
	double k = 6.9;
	double f = 5;
	double Fin = 2 * cos(2 * PI * f * t);

	dYdt[0] = Y[1]; // Y[0] = y, Y[1] = dy/dt
	dYdt[1] = 1 / m * (Fin - c * Y[1] - k * Y[0]);
}
```

## Output <br>
```c
t[0]= 0.000, y[0]= 0.000, z[0]= 0.200
t[1]= 0.010, y[1]= 0.002, z[1]= 0.205
t[2]= 0.020, y[2]= 0.004, z[2]= 0.208
t[3]= 0.030, y[3]= 0.006, z[3]= 0.207
t[4]= 0.040, y[4]= 0.008, z[4]= 0.201
t[5]= 0.050, y[5]= 0.010, z[5]= 0.190
t[6]= 0.060, y[6]= 0.012, z[6]= 0.173
t[7]= 0.070, y[7]= 0.014, z[7]= 0.152
t[8]= 0.080, y[8]= 0.015, z[8]= 0.127
t[9]= 0.090, y[9]= 0.016, z[9]= 0.100
t[10]= 0.100, y[10]= 0.017, z[10]= 0.074
```

## Warning
>* h is not 0<br>


## Error Handling
```c
if (h ==0 || tf <= t0)
{
	printf("Error: h is zero !\n");

	return;
}
```
<br>
