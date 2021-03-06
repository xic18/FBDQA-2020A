### 课程小结9 周航宇 2017010583
#### 积分
+ 积分是估值和期权定价的一个重要的数学工具。
+ 衍生品的风险中立价值一般可以用风险中立（鞅）测度下的预期折现收益来表示，这一预期在离散情况下是个总和，在连续情况下是一个积分
+ 数值积分函数库 scipy.integrate
+ 通过模拟求取积分
通过蒙特卡洛模拟的期权和衍生品估值依赖于通过模拟求取积分。在积分区间内取1个随机的x值，并计算每个随机x值处的积分函数值。加总所有函数值并求其平均值，就可以得到积分区间中的平均函数值，将该值乘以积分区间长度，以得出估算的积分值。
蒙特卡洛估算积分值随着提取的随机数个数的增加而收敛，即使提取的随机个数较少，估算值也已经相当接近。
#### 符号数学
+ sympy
~~~python
import sympy as sy
x=sy.symbols('x')
f=x**2+3+0.5*x**2+3/2
sy.simplify(f)
~~~
+ 方程式
SymPy可以求解方程，
~~~python
sy.solve(x**2-1)
sy.solve(x**2 +y**2)
~~~
+ 积分
integrate可以求出积分函数的反导数（不定积分）
~~~python
a,b=sy.symbols('a b')
print(sy.pretty(sy.Integral(sy.sin(x)+0.5*x,(x,a,b))))
int_func=sy.integrate(sy.sin(x)+0.5*x,x)
print(sy.pretty(int_func))
~~~
+ 微分
Sympy可以进行微分运算，全局最小值的必要（但不充分）条件之一是两个偏微分都为0，但是不能保证有符号解，算法和存在性问题都会影响问题的解。
#### python高性能计算库
+ numexpr 用于快速数值运算
+ multiprocessing, python内建的本地并行处理模块
+ numba，用于为CPU动态编译Python代码
+ Cython，用于合并Python和C语言静态编译泛型
~~~python
import numpy as np
import numexpr as ne
nx, ny=1200,1500
a=np.linspace(0.,3.1416,nx\*ny).reshape(nx,ny)
for i in range(100):
	b=np.sin(a+i)**2+np.cos(a+i)**2+a**1.5
	#b=ne.evaluate("sin(a+1)**2+cos(a+i)**2+a**1.5")
~~~
#### numba的优势
+ 效率：使用Numba只需花费很少的额外精力，原始函数完全不需要修改，需要做的就是调用jit函数。
+ 加速：Numba的执行速度显著提高，不仅和纯python相比如此，对向量化的numpy实现也有明显优势。
+ 内存：使用Numba不需要初始化大型数组对象：编译器专门为手上的问题生成及其代码并维持和纯python相同的内存效率。
### 如何获取Alpha
#### 股票型Alpha策略基本逻辑
+ 投资组合的建立：一部分是精选A股市场最好的股票，构建现货投资组合；另一部分是做空股指期货，利用股指期货低成本、高杠杆特性，对冲系统风险。以beta对冲为主要对冲方式，也可市值对冲。
+ 策略收益和回撤：根据历史测试，本策略提供股指期货Alpha对冲交易机会，构建股票和股指期货对冲组合。
+ 适合投资者：该策略为高风险高收益率投资策略，适合高风险偏好，中等资金规模的投资者。
#### 商品期货策略——商品套利（配对）交易策略原理
商品配对交易是利用基本面分析和量化方法寻找同一产业链或板块中商品品种间价格波动相关规律，通过做多一个品种同时，做空另外一个配对品种的交易，获得相对稳定的价差波动收益。策略一般选择品种间联动性较强的板块。
+ 跨品种套利——选择相关性较大的两个品种，当其中一个价格下跌后，做空该品种，做多另外一个品种。即发现有价差大规模下跌则做多价差，价差恢复后获利平仓。
+ 跨期套利——不同到期日的期货合约价差在一个相对稳定的区间，一旦价差出现大的波动开仓，等待价差回归后平仓止盈。
+ 产品特性跨期——利用产品特性规律最多价差，进行技术指标分析同时也会加入基本面的判断，可提高交易策略的胜率。
#### 投资交易模型基本研发流程
策略建模——追溯测试——修正错误——自动化操作。
#### 获取Alpha交易型策略的逻辑
+ 根据市场交易中出现的规律性现象，可以制定相应获利策略，称为交易型策略。
#### 多空策略
+ 交易标的：单个品种、配对价差
+ 基本逻辑假设：强者恒强，做价格（或价差）
+ HANS123
#### 回归策略
+ 交易标的：配对价差，同一标的不同表现形式
+ 基本逻辑假设：均值回复，做价差的收敛
#### ETF套利
+ 一二级市场套利
+ 二级市场轮动
+ 期现套利
+ 对冲工具的使用
	对冲工具选择：股指期货、ETF期权、股指期货。



