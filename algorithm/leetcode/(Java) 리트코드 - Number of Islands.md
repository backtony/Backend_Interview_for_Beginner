[[문제 링크](https://leetcode.com/problems/number-of-islands/)



## Java 풀이
```java
class Solution {

    private int[] dx = {-1, 0, 1, 0};
    private int[] dy = {0, 1, 0, -1};
    private int height;
    private int weight;

    public int numIslands(char[][] grid) {

        int count = 0;
        height = grid.length;
        weight = grid[0].length;

        for (int x = 0; x < height; x++) {
            for (int y = 0; y < weight; y++) {
                if (isLand(grid[x][y])) {
                    dfs(grid, x, y);
                    count++;
                }
            }
        }
        return count;
    }

    private void dfs(char[][] grid, int x, int y) {
        grid[x][y] = 0;
        for (int d = 0; d < 4; d++) {
            int px = x + dx[d];
            int py = y + dy[d];
            if (isInBound(px, py)) {
                if (isLand(grid[px][py])) {
                    dfs(grid, px, py);
                }
            }
        }
    }

    private boolean isInBound(int px, int py) {
        return 0 <= px && px < height && 0 <= py && py < weight;
    }

    private boolean isLand(char c) {
        return c == '1';
    }
}

```
