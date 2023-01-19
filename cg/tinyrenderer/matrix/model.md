## 1.平移矩阵(translate)
$$    
\left[
\begin{matrix}
1 & 0 & 0 & dx \\
0 & 1 & 0 & dy \\
0 & 0 & 1 & dz \\
0 & 0 & 0 & 1
\end{matrix}
\right] 
$$


## 2.旋转矩阵(rotate)
* 绕x轴旋转
$$    
\left[
\begin{matrix}
1& 0 & 0 & 0 \\
0 & cosa & -sina & 0 \\
0 & sina & cosa & 0 \\
0 & 0 & 0 & 1
\end{matrix}
\right] 
$$
* 绕y轴旋转
$$    
\left[
\begin{matrix}
cosa & 0 & sina & 0 \\
0 & 1 & 0 & 0 \\
-sina & 0 & cosa & 0 \\
0 & 0 & 0 & 1
\end{matrix}
\right] 
$$
* 绕z轴旋转
$$    
\left[
\begin{matrix}
cosa & -sina & 0 & 0 \\
sina & cosa & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{matrix}
\right] 
$$


## 3.缩放矩阵(scale)
$$    
\left[
\begin{matrix}
dx & 0 & 0 & 0 \\
0 & dy & 0 & 0 \\
0 & 0 & dz & 0 \\
0 & 0 & 0 & 1
\end{matrix}
\right] 
$$
