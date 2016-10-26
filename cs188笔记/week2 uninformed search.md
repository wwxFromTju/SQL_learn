# 简单介绍
讲了一些uninformed search的一些方法，就是不考虑具体的模型，直接套用通用的搜索策略
# 提纲
1. Outline：做决策就是最大化收益，要往前看，3种搜索，depth-first search，breadth-first search， uniform-cost search
2. agents that plan vs. reflex agents：plan 就是有计划， reflex 就是考虑目前，不往后看
3. search problems：表示搜索，状态空间
4. state space graphs and search trees： 用search trees来表示state space
5. tree search：从初始开始，依次扩展可以访问到的节点
6. depth-first tree search：深度优先搜索，从一个节点开始依次向下，如果不是目标节点，而且没有可以扩展的节点，然后回溯到上节点，然后扩张另外一个节点。
7. search algorithm properties：搜索问题需要考虑时间复杂度，空间复杂度，是否复杂，是否是最优解
8. depth-first tree search properties：深度优先搜索在7中的分析
9. breadth-first tree search：广度优先搜索，从一个节点出发，访问所有能访问的节点，然后在扩展所有能访问的节点
10. breadth-first tree search properties：广度优先搜索在7中的分析
11. relative advantages of breadth-first and depth-first search:分析深度优先搜索和广度优先搜索在不同环境下的优劣和取舍
12. iterative deepening：广度和深度的结合，每次限定深度，比如deep从1，2，3依次开始，在限定深度下做搜索。
13. cost-sensitive search and uniform cost search：考虑边的权值，从初始节点开始，依次加入可以访问到的最短的节点
14. search and models：在实际运用中要考虑到外界模型的影响
# 重点
