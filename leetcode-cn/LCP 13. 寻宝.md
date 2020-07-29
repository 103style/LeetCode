# [LCP 13. 寻宝](https://leetcode-cn.com/problems/xun-bao/)

---

**leetcode-cn Daily Challenge on July 29th, 2020.**

---

> **Difficulty** : **Hard**
>
> **Related Topics** : **DynamicProgramming**

---

> 我们得到了一副藏宝图，藏宝图显示，在一个迷宫中存在着未被世人发现的宝藏。
> 
> 迷宫是一个二维矩阵，用一个字符串数组表示。它标识了唯一的入口（用 'S' 表示），和唯一的宝藏地点（用 'T' 表示）。但是，宝藏被一些隐蔽的机关保护了起来。在地图上有若干个机关点（用 'M' 表示），**只有所有机关均被触发，才可以拿到宝藏**。
> 
> 要保持机关的触发，需要把一个重石放在上面。迷宫中有若干个石堆（用 'O' 表示），每个石堆都有 **无限** 个足够触发机关的重石。但是由于石头太重，我们一次只能搬一个石头到指定地点。
> 
> 迷宫中同样有一些墙壁（用 '#' 表示），我们不能走入墙壁。剩余的都是可随意通行的点（用 '.' 表示）。石堆、机关、起点和终点（无论是否能拿到宝藏）也是可以通行的。
> 
> 我们每步可以选择向上/向下/向左/向右移动一格，并且不能移出迷宫。搬起石头和放下石头不算步数。那么，从起点开始，我们最少需要多少步才能最后拿到宝藏呢？如果无法拿到宝藏，返回 -1 。
> 
> ### 示例 1：
> ```
> 输入： ["S#O", "M..", "M.T"]
> 
> 输出：16
> 
> 解释：最优路线为： S->O, cost = 4, 去搬石头 O->第二行的M, cost = 3, M机关触发 第二行的M->O, cost = 3, 我们需要继续回去 O 搬石头。 O->第三行的M, cost = 4, 此时所有机关均触发 第三行的M->T, cost = 2，去T点拿宝藏。 总步数为16。
> ```
> ![1](https://pic.leetcode-cn.com/6bfff669ad65d494cdc237bcedfec10a2b1ac2f2593c2bf97e9aecb41dc8a08b-%E5%9B%BE%E7%89%87.gif)
> 
> ### 示例 2：
> ```
> 输入： ["S#O", "M.#", "M.T"]
> 
> 输出：-1
> 
> 解释：我们无法搬到石头触发机关
> ```
> 
> ### 示例 3：
> ```
> 输入： ["S#O", "M.T", "M.."]
> 
> 输出：17
> 
> 解释：注意终点也是可以通行的。
> ```
> 
> ### 限制：
> * `1 <= maze.length <= 100`
> * `1 <= maze[i].length <= 100`
> * `maze[i].length == maze[j].length`
> * S 和 T 有且只有一个
> * 0 <= M的数量 <= 16
> * 0 <= O的数量 <= 40，题目保证当迷宫中存在 M 时，一定存在至少一个 O 。


---

### Solution
* **mine**
  * **Java**
    * ``
      ```
      ```


---


* **leetcode solution**
>  * `执行用时：92 ms, 击败了84.88%，内存消耗：44.1 MB, 在所有 Java 提交中击败了100.00%的用户`
>    ```
>    class Solution {
>        int n, m;
>
>        public int minimalSteps(String[] maze) {
>            n = maze.length;
>            m = maze[0].length();
>            // 机关 & 石头
>            List<int[]> buttons = new ArrayList<int[]>();
>            List<int[]> stones = new ArrayList<int[]>();
>            // 起点 & 终点
>            int sx = -1, sy = -1, tx = -1, ty = -1;
>            for (int i = 0; i < n; i++) {
>                for (int j = 0; j < m; j++) {
>                    if (maze[i].charAt(j) == 'M') {
>                        buttons.add(new int[]{i, j});
>                    }
>                    if (maze[i].charAt(j) == 'O') {
>                        stones.add(new int[]{i, j});
>                    }
>                    if (maze[i].charAt(j) == 'S') {
>                        sx = i;
>                        sy = j;
>                    }
>                    if (maze[i].charAt(j) == 'T') {
>                        tx = i;
>                        ty = j;
>                    }
>                }
>            }
>            int nb = buttons.size();
>            int ns = stones.size();
>            //记录起点到其他点的距离
>            int[][] startDist = bfs(sx, sy, maze);
>
>            // 边界情况：没有机关
>            if (nb == 0) {
>                return startDist[tx][ty];
>            }
>            //从某个机关到其他机关、起点、终点的最短距离
>            // dist[][0- nb-1] 机关经过石头到其他机关的最短距离
>            //dist[][nb] 起点经过石头到机关的最短距离
>            //dist[][nb+1] 机关到终点的最短距离
>            int[][] dist = new int[nb][nb + 2];
>            for (int i = 0; i < nb; i++) {
>                Arrays.fill(dist[i], -1);
>            }
>            // 记录每个机关点 到 其他点的距离
>            int[][][] dd = new int[nb][][];
>            for (int i = 0; i < nb; i++) {
>                int[][] d = bfs(buttons.get(i)[0], buttons.get(i)[1], maze);
>                dd[i] = d;
>                //当前机关到终点的最短距离
>                dist[i][nb + 1] = d[tx][ty];
>            }
>
>            for (int i = 0; i < nb; i++) {
>                //记录从 起点 到 拿石头 再到 当前机关 的最短距离
>                int tmp = -1;
>                for (int k = 0; k < ns; k++) {
>                    //当前石头的坐标
>                    int midX = stones.get(k)[0], midY = stones.get(k)[1];
>                    //当前机关能到这个石头 并且 起点能到这个石头
>                    if (dd[i][midX][midY] != -1 && startDist[midX][midY] != -1) {
>                        if (tmp == -1 || tmp > dd[i][midX][midY] + startDist[midX][midY]) {
>                            tmp = dd[i][midX][midY] + startDist[midX][midY];
>                        }
>                    }
>                }
>                //从起点 到 石头  到这个机关 的最短距离
>                dist[i][nb] = tmp;
>
>                for (int j = i + 1; j < nb; j++) {
>                    //记录 机关i 到 某个石头 再到 机关j 的最短距离
>                    int mn = -1;
>                    for (int k = 0; k < ns; k++) {
>                        //当前石头的坐标
>                        int midX = stones.get(k)[0], midY = stones.get(k)[1];
>                        // 石头到 机关i 的距离 和 石头到 机关j 的距离
>                        if (dd[i][midX][midY] != -1 && dd[j][midX][midY] != -1) {
>                            if (mn == -1 || mn > dd[i][midX][midY] + dd[j][midX][midY]) {
>                                mn = dd[i][midX][midY] + dd[j][midX][midY];
>                            }
>                        }
>                    }
>                    dist[i][j] = mn;
>                    dist[j][i] = mn;
>                }
>            }
>
>            // 无法达成的情形: 某一个机关 不能通过某一个石头 到达 另一个机关
>            for (int i = 0; i < nb; i++) {
>                if (dist[i][nb] == -1 || dist[i][nb + 1] == -1) {
>                    return -1;
>                }
>            }
>
>            //111111  每个1代表一个机关
>            // dp 数组， -1 代表没有遍历到
>            int[][] dp = new int[1 << nb][nb];
>            for (int i = 0; i < 1 << nb; i++) {
>                Arrays.fill(dp[i], -1);
>            }
>            for (int i = 0; i < nb; i++) {
>                //从 起点 到 石头 到 该机关 的最短距离
>                dp[1 << i][i] = dist[i][nb];
>            }
>
>            // 由于更新的状态都比未更新的大，所以直接从小到大遍历即可
>            for (int mask = 1; mask < (1 << nb); mask++) {
>                for (int i = 0; i < nb; i++) {
>                    // 当前 dp 是合法的,
>                    // 比如： mask = 0110  说明当前 选了 第二 第三个机关
>                    if ((mask & (1 << i)) != 0) {
>                        for (int j = 0; j < nb; j++) {
>                            // j 不在 mask 里， 找到还没有开启的机关
>                            // mask = 0110 说明就 只能选第一个和 第四个机关
>                            if ((mask & (1 << j)) == 0) {
>                                // j = 0  next = 0110 | 0001 = 0111
>                                int next = mask | (1 << j);
>                                //dist[i][j] 是指 机关i 经过 石头 到机关 j 的最短距离
>                                //dp[mask][i] 表示 mask这个值 状态下最后选择 i 机关的最短距离
>                                //dp[next][j]  表示 next这个值 状态下最后选择 j 机关的最短距离
>                                //dp[mask][j] + dist[i][j] 就等于 从 mask状态 选择从 机关i 经过石头 到机关j 到 next状态下的最短距离
>                                if (dp[next][j] == -1 || dp[next][j] > dp[mask][i] + dist[i][j]) {
>                                    dp[next][j] = dp[mask][i] + dist[i][j];
>                                }
>                            }
>                        }
>                    }
>                }
>            }
>
>            int ret = -1;
>            //finalMask = 111111  表示每个机关都打开了
>            int finalMask = (1 << nb) - 1;
>            for (int i = 0; i < nb; i++) {
>                //dp[finalMask][i] + dist[i][nb + 1] 表示 最后一个到的机关是i 然后加上 到 机关i 到 终点的最短距离
>                if (ret == -1 || ret > dp[finalMask][i] + dist[i][nb + 1]) {
>                    ret = dp[finalMask][i] + dist[i][nb + 1];
>                }
>            }
>
>            return ret;
>        }
>
>        /**
>         * 找到 (x,y)到其他点的最短距离
>         */
>        public int[][] bfs(int x, int y, String[] maze) {
>            //上下左右
>            int[] dx = {1, -1, 0, 0};
>            int[] dy = {0, 0, 1, -1};
>            int[][] ret = new int[n][m];
>            for (int i = 0; i < n; i++) {
>                Arrays.fill(ret[i], -1);
>            }
>            ret[x][y] = 0;
>            Queue<int[]> queue = new LinkedList<int[]>();
>            queue.offer(new int[]{x, y});
>            while (!queue.isEmpty()) {
>                int[] p = queue.poll();
>                int curx = p[0], cury = p[1];
>                for (int k = 0; k < 4; k++) {
>                    int nx = curx + dx[k], ny = cury + dy[k];
>                    if (inBound(nx, ny) && maze[nx].charAt(ny) != '#' && ret[nx][ny] == -1) {
>                        ret[nx][ny] = ret[curx][cury] + 1;
>                        queue.offer(new int[]{nx, ny});
>                    }
>                }
>            }
>            return ret;
>        }
>
>        public boolean inBound(int x, int y) {
>            return x >= 0 && x < n && y >= 0 && y < m;
>        }
>    }
>    ```


---
