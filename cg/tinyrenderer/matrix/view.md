> * 从世界坐标系(World Space)变化到观察空间(Camera Space)

> * 因为这里的坐标系采用的是右手系,所以相机看向世界坐标系的-z

> * view矩阵通过相机当前的位置推导出一个矩阵使其位置与原点重合，看向世界坐标系-z,相机的up朝向与世界坐标系y轴重合。这样每当对相机自身进行变化，只需推导出新的view矩阵，将其作用到相机与物体身上即可将他们变换到上述的“标准位置”，方便进行进一步的操作

## view矩阵推导
> 构建一个view矩阵，往往接受三个参数
> * 相机当前的位置position
> * 相机的朝向lookat,或者是看向的物体的位置。这里的朝向指向世界坐标系的z而不是相机的正面朝向，具体而言，对于相机p看向物体q，lookat 为p-q而不是q-p
> * 相机的上方up

一个view矩阵的构建可以拆分为三步
> 1.根据参数构建相机的坐标系
相机坐标的z轴cz即为lookat,通过up与相机的z轴可以确定一个平面，二者叉乘为相机的x轴cx，因为我们要得到三个互相垂直的轴，up与z轴，x轴未必正交，所以最后用z轴与x轴叉乘 得到相机的y轴cy


> 2.将相机平移到原点:
> 知道了相机的位置position，很容易可以得到平移矩阵
> $$
>    \left[
>    \begin{matrix}
>     1 & 0 & 0 & -px\\
>     0 & 1 & 0 & -py\\
>     0 & 0 & 1 & -pz\\
>     0 & 0 & 0 & 1
>    \end{matrix}
>    \right]
> $$ 

> 3.旋转相机的轴
> 我们的目的是通过旋转相机的轴使其与世界坐标系的轴重合，直接推导比较困难，可以先推导如何让世界坐标系的轴与相机的轴重合，即让[1,0,0],[0,1,0],[0,0,1]通过一个矩阵变换为[cx.x,cx.y,cx.z],[cy.x,cy.y,cy.z],[cz.x,cz.y,cz.z]。显然这个矩阵为
> $$
>    \left[
>    \begin{matrix}
>     cx.x & cy.x & cz.x & 0\\
>     cx.y & cy.y & cz.y & 0\\
>     cx.z & cy.z & cz.z & 0\\
>     0 & 0 & 0 & 1
>    \end{matrix}
>    \right]
> $$ 
> 所以将相机的轴与世界坐标系的轴重合的矩阵为上述矩阵的逆矩阵
> $$
>    \left[
>    \begin{matrix}
>     cx.x & cx.y & cx.z & 0\\
>     cy.x & cy.y & cy.z & 0\\
>     cz.x & cz.y & cz.z & 0\\
>     0 & 0 & 0 & 1
>    \end{matrix}
>    \right]
> $$ 

最后，将平移与旋转的矩阵组合即可得到最终的view矩阵
> $$
>    \left[
>    \begin{matrix}
>     cx.x & cx.y & cx.z & -(cx.x*px + cx.y*py + cx.z*pz)\\
>     cy.x & cy.y & cy.z & -(cy.x*px + cy.y*py + cy.z*pz)\\
>     cz.x & cz.y & cz.z & -(cz.x*px + cz.y*py + cz.z*pz)\\
>     0 & 0 & 0 & 1
>    \end{matrix}
>    \right]
> $$

我们可以对最后一列进行简化
> $$
>    \left[
>    \begin{matrix}
>     cx.x & cx.y & cx.z & -(cx.dot(p))\\
>     cy.x & cy.y & cy.z & -(cy.dot(p))\\
>     cz.x & cz.y & cz.z & -(cz.dot(p))\\
>     0 & 0 & 0 & 1
>    \end{matrix}
>    \right]
> $$

# 左手系与右手系
### 定义：
简单来说，左手系与右手系的区别就是计算向量叉乘时是用左手还是右手来判断方向
<img src="../img/10.jpg" width=300>


### 差别：
对于常见的图形学api,OpenGL使用的是右手系，Direct3D使用的是右手系,其差别体显在几个方面
> **正向旋转方向**:
> 在右手系中，正向旋转方向为逆时针，而在左手系中，正向旋转方向
> 为顺时针

> **叉积方向**:
> 在右手系中，用右手判断，左手系中，用左手判断

> **MVP变换**:
> * 对于世界坐标系，左手系与右手系都描述的是同样的物体，因此
> 不会有影响，也就是model变换没有差别
> * 但是对于view变换就不同了，比如下面的例子:
> 在(3,0,0)有一个绿色的点，在(-3,0,0)有一个红色的点,相机
> EyePos(0, 0, 15), LookAt(0, 0, 0), UpVec(0, 1, 0)
> <img src="../img/11.jpg">
> 可以看到左手系和右手系得到了左右相反的结果
## 转化：
由上述view变换的例子可知，要想左手系与右手系得到相同的结果，只需将点的x值取负即可，也就是说
## 参考
* <https://www.3dgep.com/understanding-the-view-matrix/>
* <https://learnopengl.com/Getting-started/Camera>
* <https://gamedev.stackexchange.com/questions/178643/the-view-matrix-finally-explained>

