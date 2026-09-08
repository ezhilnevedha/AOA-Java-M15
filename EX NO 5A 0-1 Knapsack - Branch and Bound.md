
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## DATE: 08.09.2026
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

For example:




## Algorithm
1. Start and sort all items in descending order of their profit/cost ratio.
2. Calculate an upper bound using the fractional knapsack idea to estimate the maximum possible profit.
3. If the calculated bound is less than or equal to the current best profit, prune that branch.
4. Otherwise, recursively explore two choices: include the current item if capacity allows, or exclude it.
5. Update best with the maximum profit found and return the optimal profit.
## Program:
```
/*
Program to implement Reverse a String
Developed by: EZHIL NEVEDHA K
Register Number:  212223230055
*/
import java.util.*;

public class StartupShowcaseOptimizer {

    // ---------- Global data ----------
    static int N, B;
    static int[] c, p;          // cost, profit after sorting by ratio
    static int best = 0;        // incumbent best profit

    // ---------- Fractional upper bound ----------
    static double bound(int idx, int cw, int cv) {
         //Type your code
         double totalProfit = (double) cv;
        int remainingCapacity = B - cw;

        for (int i = idx; i < N; i++) {
            if (c[i] <= remainingCapacity) {
                remainingCapacity -= c[i];
                totalProfit += p[i];
            } else {
                double fraction = (double) remainingCapacity / (double) c[i];
                totalProfit += fraction * p[i];
                break; 
            }
        }
        return totalProfit;
    }

    // ---------- DFS Branch & Bound ----------
    static void dfs(int idx, int cw, int cv) {
       //Type your code
       if (bound(idx, cw, cv) <= best) {
            return;
        }

        best = Math.max(best, cv);

        if (idx == N) {
            return;
        }

        if (cw + c[idx] <= B) {
            dfs(idx + 1, cw + c[idx], cv + p[idx]);
        }

        dfs(idx + 1, cw, cv);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();
        int[] cost = new int[N];
        int[] prof = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) prof[i] = sc.nextInt();
        sc.close();

        // Sort by profit/cost ratio descending → tighter bounds
        Integer[] idx = new Integer[N];
        Arrays.setAll(idx, i -> i);
        Arrays.sort(idx, Comparator.comparingDouble(i -> -(double) prof[i] / cost[i]));

        c = new int[N];
        p = new int[N];
        for (int i = 0; i < N; i++) {
            c[i] = cost[idx[i]];
            p[i] = prof[idx[i]];
        }

        dfs(0, 0, 0);
        System.out.println(best);
    }
}

```

## Output:
<img width="388" height="210" alt="image" src="https://github.com/user-attachments/assets/55d1e4c5-3244-40c0-8b08-35e6b34542d1" />



## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
