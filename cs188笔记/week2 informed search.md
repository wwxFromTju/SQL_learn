# 简单介绍
在uninformed search的基础上通过加入Heuristics等来进行优化
# 提纲
1. Outline：分为3中有信息搜索算法，heuristics，greedy search，a\*serach
2. recap：search：复习上一讲的BFS，DFS等search算法
3. informed search：加入对目的的heuristics，比如迷宫的终点的距离（曼哈顿，欧几里得等），翻煎饼的中各个的正确位置
4. greedy search：在heuristics下，只考虑当前最优
5. a\* tree search：通过混合cost和heuristics来做判断
6. admissible heuristics and a\* tree search optimality：分析在由于heuristics的性质可能导致不是最优。需要满足admissible的情况下才能获得最优解
7. proof of optimality of a\* tree search：通过一个中间节点，证明可以获得最优解
8. properties of a\*：a\* search的性质，ucs的基础上对解有一定偏向性
9. a\* applications and demos：
	- pathing／routing problems
		- video games
			- resource planning problems
			- robot motion planning
			- language analysis
			- machine translation
			- speech recognition
10. creaing admissible heuristics：一些建议关于heuristics
11. semi-Lattice of heuristics： heuristics的一些做法，比如max（a，b）
12. graph search：在tree search上发现扩展了相同的子树，所以访问过的节点加入close set，之后不再扩展close set中的节点
13. a\* graph search gone wrong：由于heuristics的设置，使得a\* graph search并不是最优解
14. consistency and optimality of a\* graph search：一个是h不能大于到目标的数值，一个是两个节点的h差值要小于等于边的cost
15. a\* optimality summary：一个是tree，一个是graph，达到最优的条件不一样
16. a\* summary：greedy 和 ucs的结合
# 重点