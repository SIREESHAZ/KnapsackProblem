# KnapsackProblem
public class KnapsackProblem {
    public static int knapsack(int[] weights, int[] values, int n, int W) {
        int[][] dp = new int[n + 1][W + 1];
        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= W; w++) {
                if (i == 0 || w == 0) {
                    dp[i][w] = 0;  // Base case: no items or capacity 0
                } else if (weights[i - 1] <= w) {
                    // Include the item or exclude it — take the maximum
                    dp[i][w] = Math.max(
                        values[i - 1] + dp[i - 1][w - weights[i - 1]], // Include item
                        dp[i - 1][w]                                   // Exclude item
                    );
                } else {
                    dp[i][w] = dp[i - 1][w];  // Can't include the item
                }
            }
        }

    
        return dp[n][W];
    }

    public static void main(String[] args) {
        int[] values = {60, 100, 120};  // Values (profits)
        int[] weights = {10, 20, 30};   // Weights
        int capacity = 50;              // Knapsack capacity
        int n = values.length;          // Number of items

        int maxProfit = knapsack(weights, values, n, capacity);
        System.out.println("Maximum Profit: " + maxProfit);
    }
}
