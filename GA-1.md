# 遗传算法：基本原理及python实现

OCT 21, 2018 • TRAIN • [GENETIC ALGORITHM](https://dothinking.github.io/blog/tagged#genetic-algorithm) [NUMPY](https://dothinking.github.io/blog/tagged#numpy) [PYTHON](https://dothinking.github.io/blog/tagged#python)

遗传算法（Genetic Algorithm）是美国J.Holland教授于1975年首先提出的借鉴生物进化规律（适者生存，优胜劣汰遗传机制）演化而来的随机化搜索方法，目前已被广泛地应用于组合优化、机器学习、信号处理、自适应控制和人工生命等领域。本文将根据其基本原理，基于Python的`Numpy`模块实现采用浮点数编码的遗传算法，用于求解单目标优化问题。

## 基本原理

经典遗传算法基本过程：

- 生成初始种群
- 选择、交叉、变异操作生成下一代种群
- 重复流程

其中一些关键术语如下：

- ```python
  种群（Population）
  ```

   

  参与演化的生物群体，即解的搜索空间

  - ```python
    个体（Individual）
    ```

     

    种群的每一个成员，对应每一个可能的解

    - `染色体（Chromosome）` 对应问题的解向量
    - `基因（Gene）` 解向量的一个分量，或者编码后的解向量的一位

  - `适应度（Fitness）` 体现个体的生存能力，与目标函数相关的函数

- ```python
  遗传算子（Operator）
  ```

   

  个体的演化操作，包括选择、交叉、变异

  - `选择(Selection)` 基于适应度的优胜劣汰，以一定的概率从种群中选择若干个体
  - `交叉(Crossover)` 两个染色体进行基因重组
  - `变异(Mutation)`：单个染色体的基因以较低概率发生随机变化

初始种群产生了一系列随机解，选择操作保证了搜索的方向性，交叉和变异拓宽了搜索空间，其中交叉操作延续父辈个体的优良基因，变异操作则可能产生比当前优势基因更优秀的个体。变异操作有利于跳出局部最优解，同时增加了随机搜索的概率，即容易发散。

遗传算法需要在过早收敛（早熟）和发散、精度和效率之间平衡。当物种多样性迅速降低即个体趋于一致，例如选择操作时过分突出优势基因的地位，结果可能只是收敛于局部最优解。当物种持续保持多样性，例如选择力度不大、变异概率太大，结果可能很难收敛，即算法效率较低。

## 程序设计

考虑程序的通用性，减少模块之间的耦合，`种群`、`遗传算子`将被设计为基本类，最后作为参数传入`遗传算法类`。参考伪代码：

```
# 基于个体生成种群
I = Individual()
P = Population(I, 50)

# 遗传算子
S = Selection()
C = Crossover()
M = Mutation()

# 综合种群和遗传算子进入遗传算法标准流程
G = GA(P, S, C, M)
res = G.run()   
```

遗传算法基本流程相对固定，因此以上结构有利于：

- 当需要改进遗传算子策略时，可以从基本算子类派生子类而不必改动其他部分
- 当需要应用于不同问题时，可以从个体基类派生相应的子类（满足编码的需要）

### 1 种群

目前仅考虑浮点数编码，因此省去了编码/解码过程——整个染色体就是解向量，每个基因是其中一个分量。

`Individual`类表征个体，重要的属性为：

- `solution` 解向量
- `evaluation` 目标函数值
- `fitness` 适应度值

`Population`类表征群体，根据个体实例生成指定大小的种群，其中：

- `individuals` 所有个体列表，`Numpy`的`ndarray`类型
- `best` 最优个体

```
#----------------------------------------------------------
# GAComponents.py: Individual, Population
#----------------------------------------------------------
import numpy as np


class Individual:
    '''individual of population'''
    def __init__(self, ranges):
        '''
        ranges: element range of solution, e.g. [(lb1, ub1), (lb2, ub2), ...]
        validation of ranges is skipped...
        '''     
        self.ranges = np.array(ranges)
        self.dimension = self.ranges.shape[0]

        # initialize solution within [lb, ub]
        seeds = np.random.random(self.dimension)
        lb = self.ranges[:, 0]
        ub = self.ranges[:, 1]
        self._solution = lb + (ub-lb)*seeds

        # evaluation and fitness
        self.evaluation = None
        self.fitness = None

    @property
    def solution(self):
        return self._solution

    @solution.setter
    def solution(self, solution):
        assert self.dimension == solution.shape[0]
        assert (solution>=self.ranges[:, 0]).all() and (solution<=self.ranges[:, 1]).all()
        self._solution = solution
    

class Population:
    '''collection of individuals'''
    def __init__(self, individual, size=50):
        '''
        individual   : individual template
        size         : count of individuals     
        '''
        self.individual = individual
        self.size = size
        self.individuals = None

    def initialize(self):
        '''initialization for next generation'''
        IndvClass = self.individual.__class__
        self.individuals = np.array([IndvClass(self.individual.ranges) for i in range(self.size)], dtype=IndvClass)

    def best(self, fun_evaluation, fun_fitness=None):
        '''get best individual according to evaluation value '''
        # evaluate first and collect evaluations
        _, evaluation = self.fitness(fun_evaluation, fun_fitness)
        # get the minimum position
        pos = np.argmin(evaluation)
        return self.individuals[pos]

    def fitness(self, fun_evaluation, fun_fitness=None):
        '''
        calculate objectibe value and fitness for each individual.
        fun_evaluation  : objective function
        fun_fitness     : population fitness based on evaluation
        '''
        # fitness is same as evaluation by default
        if not fun_fitness:
            fun_fitness = lambda x: x

        # get the value directly if it has been calculated before
        evaluation = np.array([fun_evaluation(I.solution) if I.evaluation is None else I.evaluation for I in self.individuals])

        # calculate fitness
        fitness = fun_fitness(evaluation)
        fitness = fitness/np.sum(fitness) # normalize
    
        # set attributes for each individual
        for I, e, f in zip(self.individuals, evaluation, fitness):
            I.evaluation = e
            I.fitness = f

        return fitness, evaluation


if __name__ == '__main__':

    ranges = [(-10,10)] * 3
    obj = lambda x: x[0]+x[1]**2+x[2]**3    

    I = Individual(ranges)
    P = Population(I, 100)  
    P.initialize()

    print(P.best(obj).solution)
```

### 2 遗传算子

**2.1 选择**

采用标准的`轮盘赌（RouletteWheel）`方式，以种群中个体的适应度为参考，从中选择出同样大小的新的种群个体。从上一节种群适应度的计算可知，个体的适应度已经被归一化，因此可以直接作为轮盘赌的概率参考。

```
#----------------------------------------------------------
# GAOperators.py: Selection, Crossover, Mmutation
#----------------------------------------------------------
import numpy as np
import copy
from GAComponents import Individual

#----------------------------------------------------------
# SELECTION
#----------------------------------------------------------
class Selection:
    '''base class for selection'''
    def select(self, population, fitness):
        raise NotImplementedError


class RouletteWheelSelection(Selection):
    '''
    select individuals by Roulette Wheel:
    individuals selected with a probability of its fitness
    ''' 
    def select(self, population, fitness):
        selected_individuals = np.random.choice(population.individuals, population.size, p=fitness)
        # pay attention to deep copy these objects
        population.individuals = np.array([copy.deepcopy(I) for I in selected_individuals])
```

**2.2 交叉**

从选择后的样本中随机选择两个个体`a`和`b`，以一定的概率进行交叉操作：将随机位置的对应基因（例如gaga，gbgb）按系数αα进行线性插值，其余位置保持不变，从而得到两个新的个体`a'`和`b'`。

对于交叉位置的基因：



g′ag′b=ga+(gb−ga)(1−α)=gb−(gb−ga)(1−α)ga′=ga+(gb−ga)(1−α)gb′=gb−(gb−ga)(1−α)



对于非交叉位置的基因：



g′ag′b=ga=gbga′=gagb′=gb



综合起来，个体`a`和`b`所有位置的基因交叉操作可以写成向量形式：



a′b′=a+(b−a)(1−α)β=b−(b−a)(1−α)βa′=a+(b−a)(1−α)βb′=b−(b−a)(1−α)β



其中，ββ表示是否进行交叉的`0-1`向量。

```
# ......接上一段代码

#----------------------------------------------------------
# CROSSOVER
#----------------------------------------------------------
class Crossover:
    def __init__(self, rate=0.8, alpha=0.5):
        '''
        crossover operation:
            rate: propability of crossover.
            alpha: factor for crossing two chroms, [0,1]
        '''
        # parameters check is skipped
        self.rate = rate
        self.alpha = alpha

    @staticmethod
    def cross_individuals(individual_a, individual_b, alpha):
        '''
        generate two child individuals based on parent individuals:
        new values are calculated at random positions
        alpha: linear ratio to cross two genes, exchange two genes if alpha is 0.0
        '''
        # random positions to be crossed
        pos = np.random.rand(individual_a.dimension) <= 0.5

        # cross value
        temp = (individual_b.solution-individual_a.solution)*pos*(1-alpha)
        new_value_a = individual_a.solution + temp
        new_value_b = individual_b.solution - temp

        # return new individuals
        new_individual_a = Individual(individual_a.ranges)
        new_individual_b = Individual(individual_b.ranges)

        new_individual_a.solution = new_value_a
        new_individual_b.solution = new_value_b

        return new_individual_a, new_individual_b

    def cross(self, population):

        new_individuals = []        
        random_population = np.random.permutation(population.individuals) # random order
        num = int(population.size/2.0)+1

        for individual_a, individual_b in zip(population.individuals[0:num+1], random_population[0:num+1]):         
            # crossover
            if np.random.rand() <= self.rate:
                child_individuals = self.cross_individuals(individual_a, individual_b, self.alpha)
                new_individuals.extend(child_individuals)
            else:
                new_individuals.append(individual_a)
                new_individuals.append(individual_b)

        population.individuals = np.array(new_individuals[0:population.size+1])
```

**2.3 变异**

浮点数编码个体的变异操作为将随即位置的基因`g`增加或减少一个随机值。这个随机值由允许变化区间乘以一个[0,1]区间的随机数αα来确定。例如基因`g`的区间为`[L,U]`，则变异后的基因`g'`：



gg=g−(g−L)α(rand()≤0.5)=g+(U−g)α(rand()>0.5)g=g−(g−L)α(rand()≤0.5)g=g+(U−g)α(rand()>0.5)



```
# ......接上一段代码

#----------------------------------------------------------
# MUTATION
#----------------------------------------------------------
class Mutation:
    def __init__(self, rate):
        '''
        mutation operation:
        rate: propability of mutation, [0,1]
        '''
        self.rate = rate

    def mutate_individual(self, individual, positions, alpha):
        '''
        positions: mutating gene positions, list
        alpha: mutatation magnitude
        '''
        for pos in positions:
            if np.random.rand() < 0.5:
                individual.solution[pos] -= (individual.solution[pos]-individual.ranges[:,0][pos])*alpha
            else:
                individual.solution[pos] += (individual.ranges[:,1][pos]-individual.solution[pos])*alpha
                
        # reset evaluation
        individual.evaluation = None 
        individual.fitness = None 

    
    def mutate(self, population, alpha):
        '''
        alpha: mutating magnitude
        '''
        for individual in population.individuals:
            if np.random.rand() > self.rate:
                continue

            # select random positions to mutate
            num = np.random.randint(individual.dimension) + 1
            pos = np.random.choice(individual.dimension, num, replace=False)
            self.mutate_individual(individual, pos, alpha)
```

### 3 遗传算法

本次实现的遗传算法默认求最小值，因此适应度函数应为目标函数值的反函数。并且考虑到它将作为选择概率，即函数值应非负。于是，此处设置为如下形式：

f(x)=arctan(−x)+πf(x)=arctan⁡(−x)+π

```
#----------------------------------------------------------
# GA.py: Simple Genetic Algorithm
#----------------------------------------------------------
import numpy as np


class GA():
    '''Simple Genetic Algorithm'''
    def __init__(self, population, selection, crossover, mutation, fun_fitness=lambda x:np.arctan(-x)+np.pi):
        '''
        fun_fitness: fitness based on objective values. minimize the objective by default
        '''
        self.population = population
        self.selection = selection
        self.crossover = crossover
        self.mutation = mutation
        self.fun_fitness = fun_fitness

    def run(self, fun_evaluation, gen=50):
        '''
        solve the problem based on Simple GA process
        '''

        # initialize population
        self.population.initialize()

        # solving process
        for n in range(1, gen+1):
            # select
            fitness, _ = self.population.fitness(fun_evaluation, self.fun_fitness)
            self.selection.select(self.population, fitness)

            # crossover
            self.crossover.cross(self.population)

            # mutation
            self.mutation.mutate(self.population, np.random.rand())

        # return the best individual
        return self.population.best(fun_evaluation, self.fun_fitness)
```

## 测试

采用二元函数`Schaffer_N4`进行测试，最小值点f(0,1.25313)=0.292579f(0,1.25313)=0.292579。

f(x,y)=0.5+cos2[sin(|x2−y2|)]−0.5[1+0.001(x2+y2)]2(−10≤(x,y)≤10)f(x,y)=0.5+cos2⁡[sin⁡(|x2−y2|)]−0.5[1+0.001(x2+y2)]2(−10≤(x,y)≤10)

![img](https://dothinking.github.io/blog//images/2018-10-21-01.jpg)

```
#----------------------------------------------------------
# test.py
#----------------------------------------------------------
from GAComponents import Individual, Population
from GAOperators import RouletteWheelSelection, Crossover, Mutation

# schaffer-N4
# sol: x=[0,1.25313], min=0.292579
schaffer_n4 = lambda x: 0.5 + (np.cos(np.sin(abs(x[0]**2-x[1]**2)))**2-0.5) / (1.0+0.001*(x[0]**2+x[1]**2))**2  

I = Individual([(-10,10)]*2)
P = Population(I, 50)
S = RouletteWheelSelection()
C = Crossover(0.9, 0.75)
M = Mutation(0.2)
g = GA(P, S, C, M)

res = []
for i in range(10):
    res.append(g.run(schaffer_n4, 500).evaluation)

val = schaffer_n4([0,1.25313])
val_ga = sum(res)/len(res)

print('the minimum: {0}'.format(val))
print('the GA minimum: {0}'.format(val_ga))
print('error: {:<3f} %'.format((val_ga/val-1.0)*100))

#----------------------------------------------------------
# output:
#----------------------------------------------------------
the minimum: 0.29257863204552975
the GA minimum: 0.30069849785520314
error: 2.7752764283927034 %
```

运行10次的平均误差在`3%`左右，还有很大的改进空间，这将在后续篇章中完成。

- [遗传算法：改进方向之自适应策略](https://dothinking.github.io/blog//2018/10/25/%E9%81%97%E4%BC%A0%E7%AE%97%E6%B3%95-%E6%94%B9%E8%BF%9B%E6%96%B9%E5%90%91%E4%B9%8B%E8%87%AA%E9%80%82%E5%BA%94%E7%AD%96%E7%95%A5.html)
- [遗传算法：改进方向之精英策略](https://dothinking.github.io/blog//2018/10/27/%E9%81%97%E4%BC%A0%E7%AE%97%E6%B3%95-%E6%94%B9%E8%BF%9B%E6%96%B9%E5%90%91%E4%B9%8B%E7%B2%BE%E8%8B%B1%E7%AD%96%E7%95%A5.html)

## 参考资料

[1] [遗传算法GA(Genetic Algorithm)入门知识梳理](https://segmentfault.com/a/1190000004155021#articleHeader18)

[2] [遗传算法详解（GA）](https://blog.csdn.net/u010451580/article/details/51178225)

[3] [算法理解-遗传算法（Genetic Algorithm）](https://blog.csdn.net/qq_27755195/article/details/56597467)

[4] [遗传算法中几种不同选择算子](https://zhuanlan.zhihu.com/p/29474851)





# 遗传算法(Genetic Algorithm ,GA)学习笔记

![img](https://upload.jianshu.io/users/upload_avatars/10947003/e87ab48a-37c6-44b2-9423-3b7c7d4e68c4?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)

[肥了个大西瓜](https://www.jianshu.com/u/1ed8e91cd532)关注

0.5792018.06.06 09:48:21字数 6,292阅读 2,007





## 1 遗传算法的概念

### 1.1 遗传算法的科学定义

  **遗传算法（Genetic Algorithm, GA）** 是模拟达尔文生物进化论的自然选择和遗传学机理的生物进化过程的计算模型，是一种通过**模拟自然进化过程搜索最优解的方法** 。

  其主要特点是:

  1.直接对结构对象进行操作，不存在求导和函数连续性的限定；

  2.具有内在的隐并行性和更好的全局寻优能力；

  3.采用概率化的寻优方法，**不需要确定的规则就能自动获取和指导优化的搜索空间，自适应地调整搜索方向**。

  遗传算法以一种群体中的所有个体为对象，并利用随机化技术指导一个被编码的参数空间进行高效搜索。其中，选择、交叉和变异构成了遗传算法的遗传操作；**参数编码、初始群体的设定、适应度函数的设计、遗传操作设计、控制参数设定五个要素**组成了遗传算法的核心内容。

### 1.2 遗传算法的执行过程

  遗传算法是从代表问题可能潜在的解集的一个种群（population）开始的，而一个种群则由经过基因（gene）编码的一定数目的个体(individual)组成。**每个个体实际上是染色体(chromosome)带有特征的实体** 。

  染色体作为遗传物质的主要载体，即多个基因的集合，其内部表现（即基因型）是某种基因组合，它决定了个体的形状的外部表现，如黑头发的特征是由染色体中控制这一特征的某种基因组合决定的。**因此，在一开始需要实现从表现型到基因型的映射即编码工作** 。由于仿照基因编码的工作很复杂，我们往往进行简化，如二进制编码。

  初代种群产生之后，按照适者生存和优胜劣汰的原理，逐代（generation）演化产生出越来越好的近似解，**在每一代，根据问题域中个体的适应度（fitness）大小选择（selection）个体，并借助于自然遗传学的遗传算子（genetic operators）进行组合交叉（crossover）和变异（mutation），产生出代表新的解集的种群**。

  这个过程将导致种群像自然进化一样的后生代种群比前代更加适应于环境，**末代种群中的最优个体经过解码（decoding），可以作为问题近似最优解** 。

### 1.3 遗传算法过程图解



![img](https://upload-images.jianshu.io/upload_images/10947003-b234b30997157374.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/640/format/webp)

遗传算法过程图解



## 2 相关生物学术语

  为了大家更好了解遗传算法，在此之前先简单介绍一下相关生物学术语，大家了解一下即可。

  基因型(genotype)：性状染色体的内部表现。

  表现型(phenotype)：染色体决定的性状的外部表现，或者说，根据基因型形成的个体的外部表现。

  进化(evolution)：种群逐渐适应生存环境，品质不断得到改良。生物的进化是以种群的形式进行的。

  适应度(fitness)：度量某个物种对于生存环境的适应程度。

  选择(selection)：以一定的概率从种群中选择若干个个体。一般，选择过程是一种基于适应度的优胜劣汰的过程。

  复制(reproduction)：细胞分裂时，遗传物质DNA通过复制而转移到新产生的细胞中，新细胞就继承了旧细胞的基因。

  交叉(crossover)：两个染色体的某一相同位置处DNA被切断，前后两串分别交叉组合形成两个新的染色体。也称基因重组或杂交。

  变异(mutation)：复制时可能（很小的概率）产生某些复制差错，变异产生新的染色体，表现出新的性状。

  编码(coding)：DNA中遗传信息在一个长链上按一定的模式排列。遗传编码可看作从表现型到基因型的映射。

  解码(decoding)：基因型到表现型的映射。

  个体(individual):指染色体带有特征的实体。

  种群(population:个体的集合，该集合内个体数称为种群。



## 3 实现流程

  遗传算法中每一条染色体，对应着遗传算法的一个解决方案，一般我们用适应性函数（fitness function）来衡量这个解决方案的优劣。所以从一个基因组到其解的适应度形成一个映射。遗传算法的实现过程实际上就像自然界的进化过程那样。

  下面我们用袋鼠跳中的步骤一一对应解释，以方便大家理解：

  1) 首先寻找一种对问题潜在解进行“数字化”编码的方案。（建立表现型和基因型的映射关系）

  2) 随机初始化一个种群（那么第一批袋鼠就被随意地分散在山脉上），种群里面的个体就是这些数字化的编码。

  3) 接下来，通过适当的解码过程之后（得到袋鼠的位置坐标）。

  4) 用适应性函数对每一个基因个体作一次适应度评估（袋鼠爬得越高当然就越好，所以适应度相应越高）。

  5) 用选择函数按照某种规定择优选择（每隔一段时间，射杀一些所在海拔较低的袋鼠，以保证袋鼠总体数目持平。）

  6) 让个体基因变异（让袋鼠随机地跳一跳）。

  7) 然后产生子代（希望存活下来的袋鼠是多产的，并在那里生儿育女）。

  遗传算法并不保证你能获得问题的最优解，但是使用遗传算法的最大优点在于你不必去了解和操心如何去“找”最优解。（你不必去指导袋鼠向那边跳，跳多远。）而只要简单的“否定”一些表现不好的个体就行了。（把那些总是爱走下坡路的袋鼠射杀，这就是遗传算法的精粹！）

  由此我们可以得出遗传算法的一般步骤：

  1) 随机产生种群。

  2) 根据策略判断个体的适应度，是否符合优化准则，若符合，输出最佳个体及其最优解，结束。否则，进行下一步。

  3) 依据适应度选择父母，适应度高的个体被选中的概率高，适应度低的个体被淘汰。

  4) 用父母的染色体按照一定的方法进行交叉，生成子代。

  5) 对子代染色体进行变异。

  6) 由交叉和变异产生新一代种群，返回步骤2，直到最优解产生。



## 4 实现细节(以求解一元函数最大值为例）

### 4.1 编码

  编码是应用遗传算法时要解决的首要问题，也是设计遗传算法时的一个关键步骤。**编码方法影响到交叉算子、变异算子等遗传算子的运算方法，很大程度上决定了遗传进化的效率** 。

  迄今为止人们已经提出了许多种不同的编码方法。总的来说，**这些编码方法可以分为三大类：二进制编码法、浮点编码法、符号编码法** 。下面分别进行介绍。

#### 4.1.1 二进制编码

  就像人类的基因有AGCT 4种碱基序列一样。不过在这里我们只用了0和1两种碱基,然后将它们串成一条链形成染色体。一个位能表示出2种状态的信息量，因此足够长的二进制染色体便能表示所有的特征。这便是二进制编码。如下：

  1110001010111

  它由二进制符号0和1所组成的二值符号集。它有以下一些优点：

  **1）编码、解码操作简单易行**

  **2）交叉、变异等遗传操作便于实现**

  3）合最小字符集编码原则

  4）利用模式定力对算法进行理论分析

  二进制编码的缺点是：对于一些连续函数的优化问题，由于其随机性使得其局部搜索能力较差，如对于一些高精度的问题（如上题），**当解迫近于最优解后，由于其变异后表现型变化很大，不连续，所以会远离最优解，达不到稳定**。

#### 4.1.2 浮点编码法

  二进制编码虽然简单直观，一目了然。但是存在着连续函数离散化时的映射误差。**个体长度较短时，可能达不到精度要求，而个体编码长度较长时，虽然能提高精度，但增加了解码的难度，使遗传算法的搜索空间急剧扩大**。

  **所谓浮点法，是指个体的每个基因值用某一范围内的一个浮点数来表示**。在浮点数编码方法中，必须保证基因值在给定的区间限制范围内，遗传算法中所使用的交叉、变异等遗传算子也必须保证其运算结果所产生的新个体的基因值也在这个区间限制范围内。如下所示：

  **1.2-3.2-5.3-7.2-1.4-9.7**

  浮点数编码方法有下面几个优点：

  1) 适用于在遗传算法中表示范围较大的数。

  2) 适用于精度要求较高的遗传算法。

  3) 便于较大空间的遗传搜索。

  4) 改善了遗传算法的计算复杂性，提高了运算交率。

  5) 便于遗传算法与经典优化方法的混合使用。

  6) 便于设计针对问题的专门知识的知识型遗传算子。

  7) 便于处理复杂的决策变量约束条件。

#### 4.1.3 符号编码法

  符号编码法是指个体染色体编码串中的基因值取自一个无数值含义、而只有代码含义的符号集如｛A,B,C…｝。

  符号编码的主要优点是：

  1) 符合有意义积术块编码原则。

  2) 便于在遗传算法中利用所求解问题的专门知识。

  3) 便于遗传算法与相关近似算法之间的混合使用。

### 4.2 对解的编码（以求解一元函数最大值为例）

  我们将求解一元函数最大值问题的解视为袋鼠蹦跳的问题，那么，如何利用上面的编码来为我们的袋鼠染色体编码呢？首先我们要明确一点：**编码无非就是建立从基因型到表现型的映射关系**。这里的表现型可以理解为个体特征（比如身高、体重、毛色等等）。那么，在此问题下，**我们关心的个体特征就是：袋鼠的位置坐标（因为我们要把海拔低的袋鼠给杀掉）**。无论袋鼠长什么样，爱吃什么。我们关心的始终是袋鼠在哪里，并且只要知道了袋鼠的位置坐标 **（位置坐标就是相应的染色体编码，可以通过解码得出）**，我们就可以：

  **1) 在喜马拉雅山脉的地图上找到相应的位置坐标，算出海拔高度。（相当于通过自变量求得适应函数的值）然后判读该不该射杀该袋鼠。**

  **2) 可以知道染色体交叉和变异后袋鼠新的位置坐标。**

  在一元函数求解最大值的问题中，**我们把极大值比喻为山峰，那么，袋鼠的位置坐标可以比喻为区间[-1, 2]的某一个x坐标（有了x坐标，再通过函数表达式可以算出函数值 <==> 得到了袋鼠染色体编码，解码得到位置坐标，在喜马拉雅山脉地图查询位置坐标算出海拔高度）**。这个x坐标是一个实数，现在，说白了就是怎么对这个x坐标进行编码。下面我们以二进制编码为例讲解，不过这种情况下以二进制编码比较复杂就是了。（如果以浮点数编码，其实就很简洁了，就一浮点数而已。）

  **我们说过，一定长度的二进制编码序列，只能表示一定精度的浮点数。** 在这里假如我们要求解精确到六位小数，由于区间长度为2 - (-1) = 3 ,为了保证精度要求，至少把区间[-1,2]分为3 × 10^6等份。又因为

  2^21 = 2097152 < 3*10^6 < 2^22 = 4194304

  **所以编码的二进制串至少需要22位。**

  把一个二进制串(b0,b1,....bn)转化为区间里面对应的实数值可以通过下面两个步骤：

  1）将一个二进制串代表的二进制数转化为10进制数



![img](https://upload-images.jianshu.io/upload_images/10947003-6cb2641dd9053b8f.png?imageMogr2/auto-orient/strip|imageView2/2/w/289/format/webp)

  2）对应区间内的实数：



![img](https://upload-images.jianshu.io/upload_images/10947003-aa162cf8fc677ef6.png?imageMogr2/auto-orient/strip|imageView2/2/w/191/format/webp)

  例如一个二进制串(1000101110110101000111)通过上面换算以后，表示实数值0.637197。

  好了，上面的编码方式只是举个例子让大家更好理解而已，**编码的方式千奇百怪，层出不穷，每个问题可能采用的编码方式都不一样。** 在这一点上大家要注意。

### 4.3 评价个体的适应度

  前面说了，**适应度函数主要是通过个体特征从而判断个体的适应度** 。在本例的袋鼠跳中，我们只关心袋鼠的海拔高度，以此来判断是否该射杀该袋鼠。这样一来，该函数就非常简单了。**只要输入袋鼠的位置坐标，在通过相应查找运算，返回袋鼠当前位置的海拔高度就行**。

  适应度函数也称评价函数，是根据目标函数确定的用于区分群体中个体好坏的标准。**适应度函数总是非负的，而目标函数可能有正有负，故需要在目标函数与适应度函数之间进行变换**。

  评价个体适应度的一般过程为：

  1. 对个体编码串进行解码处理后，可得到个体的表现型。

  2. 由个体的表现型可计算出对应个体的目标函数值。

  3. 根据最优化问题的类型，由目标函数值按一定的转换规则求出个体的适应度。

### 4.4 选择个体

  **遗传算法中的选择操作就是用来确定如何从父代群体中按某种方法选取那些个体，以便遗传到下一代群体**。选择操作用来确定重组或交叉个体，以及被选个体将产生多少个子代个体。前面说了，我们希望海拔高的袋鼠存活下来，并尽可能繁衍更多的后代。但我们都知道，在自然界中，适应度高的袋鼠越能繁衍后代，但这也是从概率上说的而已。毕竟有些适应度低的袋鼠也可能逃过我们的眼睛。

#### 4.4.1 选择个体的方法

  那么，怎么建立这种概率关系呢？

  下面介绍几种常用的选择算子：

  **1. 轮盘赌选择（Roulette Wheel Selection）**：是一种回放式随机采样方法。每个个体进入下一代的概率等于它的适应度值与整个种群中个体适应度值和的比例。选择误差较大。

  **2. 随机竞争选择（Stochastic Tournament）**：每次按轮盘赌选择一对个体，然后让这两个个体进行竞争，适应度高的被选中，如此反复，直到选满为止。

  **3. 最佳保留选择**：首先按轮盘赌选择方法执行遗传算法的选择操作，然后将当前群体中适应度最高的个体结构完整地复制到下一代群体中。

  **4. 无回放随机选择（也叫期望值选择Excepted Value Selection）**：根据每个个体在下一代群体中的生存期望来进行随机选择运算。方法如下:

  （1） 计算群体中每个个体在下一代群体中的生存期望数目N。

  （2） 若某一个体被选中参与交叉运算，则它在下一代中的生存期望数目减去 0.5，若某一个体未被选中参与交叉运算，则它在下一代中的生存期望数目减去1.0。

  （3） 随着选择过程的进行，若某一个体的生存期望数目小于0时，则该个体就不再有机会被选中。

  **5. 确定式选择**：按照一种确定的方式来进行选择操作。具体操作过程如下：

  （1）计算群体中各个个体在下一代群体中的期望生存数目N。

  （2）用N的整数部分确定各个对应个体在下一代群体中的生存数目。

  （3）用N的小数部分对个体进行降序排列，顺序取前M个个体加入到下一代群体中。至此可完全确定出下一代群体中Ｍ个个体。

  **6. 无回放余数随机选择**：可确保适应度比平均适应度大的一些个体能够被遗传到下一代群体中，因而选择误差比较小。

  **7. 均匀排序**：对群体中的所有个体按期适应度大小进行排序，基于这个排序来分配各个个体被选中的概率。

  **8. 最佳保存策略**：当前群体中适应度最高的个体不参与交叉运算和变异运算，而是用它来代替掉本代群体中经过交叉、变异等操作后所产生的适应度最低的个体。

  **9. 随机联赛选择**：每次选取几个个体中适应度最高的一个个体遗传到下一代群体中。

  **10. 排挤选择**：新生成的子代将代替或排挤相似的旧父代个体，提高群体的多样性。

#### 4.4.2 个体选择方法示例

  下面以轮盘赌选择为例给大家讲解一下：

  假如有５条染色体，他们的适应度分别为５、８、３、７、２。

  那么总的适应度为：F = 5 + 8 + 3 + 7 + 2 = 25。

  那么各个个体的被选中的概率为：

  α1 = ( 5 / 25 ) * 100% = 20%

  α2 = ( 8 / 25 ) * 100% = 32%

  α3 = ( 3 / 25 ) * 100% = 12%

  α4 = ( 7 / 25 ) * 100% = 28%

  α5 = ( 2 / 25 ) * 100% = 8%

  所以转盘如下：



![img](https://upload-images.jianshu.io/upload_images/10947003-eae38620364d5266.png?imageMogr2/auto-orient/strip|imageView2/2/w/502/format/webp)

  **当指针在这个转盘上转动，停止下来时指向的个体就是天选之人啦。可以看出，适应性越高的个体被选中的概率就越大。**

### 4.5 遗传--染色体交叉(crossover)

  **遗传算法的交叉操作，是指对两个相互配对的染色体按某种方式相互交换其部分基因，从而形成两个新的个体。**

  适用于二进制编码个体或浮点数编码个体的交叉算子：

  **1. 单点交叉（One-point Crossover）**：指在个体编码串中只随机设置一个交叉点，然后再该点相互交换两个配对个体的部分染色体。

  **2. 两点交叉与多点交叉：**

  (1) 两点交叉（Two-point Crossover）：在个体编码串中随机设置了两个交叉点，然后再进行部分基因交换。

  (2) 多点交叉（Multi-point Crossover）

  **3. 均匀交叉（也称一致交叉，Uniform Crossover）**：两个配对个体的每个基因座上的基因都以相同的交叉概率进行交换，从而形成两个新个体。

  **4. 算术交叉（Arithmetic Crossover）**：由两个个体的线性组合而产生出两个新的个体。该操作对象一般是由浮点数编码表示的个体。

  二进制编码的染色体交叉过程非常类似高中生物中所讲的同源染色体的联会过程――**随机把其中几个位于同一位置的编码进行交换，产生新的个体。**



![img](https://upload-images.jianshu.io/upload_images/10947003-9336bf27b301575b.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/264/format/webp)

  对应的二进制交叉：



![img](https://upload-images.jianshu.io/upload_images/10947003-7fd2fa0f4af6d30e.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/491/format/webp)

### 4.6 变异--基因突变(Mutation)

  遗传算法中的变异运算，是指将个体染色体编码串中的某些基因座上的基因值用该基因座上的其它等位基因来替换，从而形成新的个体。

  例如下面这串二进制编码：

101101001011001

  经过基因突变后，可能变成以下这串新的编码：



![img](https://upload-images.jianshu.io/upload_images/10947003-206b698572b14f8b.png?imageMogr2/auto-orient/strip|imageView2/2/w/390/format/webp)

  以下变异算子适用于二进制编码和浮点数编码的个体：

  **1. 基本位变异（Simple Mutation）**：对个体编码串中以变异概率、随机指定的某一位或某几位仅因座上的值做变异运算。

  **2. 均匀变异（Uniform Mutation）**：分别用符合某一范围内均匀分布的随机数，以某一较小的概率来替换个体编码串中各个基因座上的原有基因值。（特别适用于在算法的初级运行阶段）

  **3. 边界变异（Boundary Mutation）**：随机的取基因座上的两个对应边界基因值之一去替代原有基因值。特别适用于最优点位于或接近于可行解的边界时的一类问题。

  **4. 非均匀变异**：对原有的基因值做一随机扰动，以扰动后的结果作为变异后的新基因值。对每个基因座都以相同的概率进行变异运算之后，相当于整个解向量在解空间中作了一次轻微的变动。

  **5. 高斯近似变异**：进行变异操作时用符号均值为Ｐ的平均值，方差为P**2的正态分布的一个随机数来替换原有的基因值。





## Code：

1. [用遗传算法(Genetic Algorithm)求解一元函数最大值问题](https://github.com/IngridLiu/Notebook/blob/master/OptimizationAlgorithm/3.1%20Genetic%20Algorithm/GA_MaxNum.cpp)
2. [用遗传算法(Genetic Algorithm)求解TSP问题](https://github.com/IngridLiu/Notebook/tree/master/OptimizationAlgorithm/3.1%20Genetic%20Algorithm/TSPGeneticAlgorithm)













## Reference:

1. [干货 | 遗传算法(Genetic Algorithm) （附代码及注释）](https://mp.weixin.qq.com/s?__biz=MzIyNzg5MTQ5Mg==&mid=2247484529&idx=1&sn=6137baf119a703a094283dff364a228b&chksm=e85b043adf2c8d2c2e191ac228557a6b8253b0cc5d9ae451619b902ec559c354adbef689e9b5&scene=21#wechat_redirect)
2. [嘿！你和遗传算法的距离也许只差这一文(附C++代码和详细代码注释)](https://mp.weixin.qq.com/s?__biz=MzIyNzg5MTQ5Mg==&mid=2247484044&idx=1&sn=e55f74a4a77681d9729fda4713d3a6a8&chksm=e85b02c7df2c8bd1b7f1293032b70686daf2a61b54561c04fafb339c6895eef5a0fdcea58e55&scene=21#wechat_redirect)
3. [遗传算法(Genetic Algorithm) Java 详细代码及注释](https://github.com/IngridLiu/Notebook/tree/master/OptimizationAlgorithm/3.1%20Genetic%20Algorithm/TSPGeneticAlgorithm)