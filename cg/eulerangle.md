## 1.定义
> * 静态定义:
欧拉角用三个角度值表示一个oritentation
> * 动态定义：
欧拉角将一次旋转，或者说将一个角位移表示为绕着三个互相垂直的旋转序列

## 2.内旋与外旋
动态定义中的旋转有两种方式，内旋与外旋
> * 内旋：绕着刚体自身的体轴进行旋转
> * 外旋: 绕着一个固定坐标系旋转

内旋与外旋是等效的，只要按照相反的顺序进行旋转
证明：
![](img/15.PNG)
![](img/16.PNG)
![](img/17.PNG)
![](img/18.PNG)

欧拉角一般具有两大类表示方式,每类按照旋转次序的不同分为6小类:

> * (经典欧拉角)Proper Euler angles
>    第一次与第三次旋转轴相同
>    (z-x-z,x-y-x, y-z-y, z-y-z, x-z-x, y-x-y)

> * (泰特布莱恩角)Tait–Bryan angles
>    三次旋转轴都不同 
>    (x-y-z,y-z-x, z-x-y, x-z-y, z-y-x, y-x-z)

## 3.术语
![](img/19.png)

## [4.万向节死锁(Gimbal Lock)](gimbalLock.md)


## 参考
> * 3D数学基础：图形和游戏开发第2版
> * [wiki](https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%8B%89%E8%A7%92)