<h1>2503. Maximum Number of Points From Grid Queries</h1>

<h2>Problem Statement</h2>
<p>You are given an <code>m x n</code> integer matrix <code>grid</code> and an array <code>queries</code> of size <code>k</code>.</p>
<p>Find an array <code>answer</code> of size <code>k</code> such that for each integer <code>queries[i]</code> you start in the top-left cell of the matrix and repeat the following process:</p>
<ul>
<li>If <code>queries[i]</code> is strictly greater than the value of the current cell that you are in, then you get one point if it is your first time visiting this cell, and you can move to any adjacent cell in all 4 directions: up, down, left, and right.</li>
<li>Otherwise, you do not get any points, and you end this process.</li>
<li>After the process, <code>answer[i]</code> is the maximum number of points you can get. Note that for each query you are allowed to visit the same cell multiple times.</li>
</ul>
<p>Return the resulting array <code>answer</code>.</p>

<h2>Example 1:</h2>
<pre>
Input: grid = [[1,2,3],[2,5,7],[3,5,1]], queries = [5,6,2]
Output: [5,8,1]
</pre>

<h2>Example 2:</h2>
<pre>
Input: grid = [[5,2,1],[1,1,2]], queries = [3]
Output: [0]
</pre>

<h2>Constraints:</h2>
<ul>
<li><code>2 <= m, n <= 1000</code></li>
<li><code>4 <= m * n <= 10^5</code></li>
<li><code>1 <= k <= 10^4</code></li>
<li><code>1 <= grid[i][j], queries[i] <= 10^6</code></li>
</ul>

<h2>Solution</h2>
<pre><code class="language-python">from dataclasses import dataclass
import heapq

@dataclass(frozen=True)
class IndexedQuery:
  queryIndex: int
  query: int
  def __iter__(self):
    yield self.queryIndex
    yield self.query

class Solution:
  def maxPoints(self, grid: list[list[int]], queries: list[int]) -> list[int]:
    DIRS = ((0, 1), (1, 0), (0, -1), (-1, 0))
    m = len(grid)
    n = len(grid[0])
    ans = [0] * len(queries)
    minHeap = [(grid[0][0], 0, 0)]  # (grid[i][j], i, j)
    seen = {(0, 0)}
    accumulate = 0

    for queryIndex, query in sorted([IndexedQuery(i, query)
                                     for i, query in enumerate(queries)],
                                    key=lambda x: x.query):
      while minHeap:
        val, i, j = heapq.heappop(minHeap)
        if val >= query:
          heapq.heappush(minHeap, (val, i, j))
          break
        accumulate += 1
        for dx, dy in DIRS:
          x = i + dx
          y = j + dy
          if x < 0 or x == m or y < 0 or y == n:
            continue
          if (x, y) in seen:
            continue
          heapq.heappush(minHeap, (grid[x][y], x, y))
          seen.add((x, y))
      ans[queryIndex] = accumulate
    return ans</code></pre>
