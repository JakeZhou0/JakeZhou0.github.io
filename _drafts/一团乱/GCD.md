## 问题描述

给定两个不同的正整数 $a, b$，求一个正整数 $k$ 使得 $gcd(a+k, b+k)$ 尽可能大，其中 $gcd(a, b)$ 表示 $a$ 和 $b$ 的最大公约数。如果存在多个 $k$，请输出所有满足条件的 $k$ 中最小的那个。

## 输入格式

输入一行包含两个正整数 $a, b$，用一个空格分隔。

## 输出格式

输出一行包含一个正整数 $k$。

## 样例输入

```
5 7
```

## 样例输出

```
1
```

## 说明

- 对于 20% 的评测用例，$1 ≤ a < b ≤ 10^5$；
- 对于 40% 的评测用例，$1 ≤ a < b ≤ 10^9$；
- 对于所有评测用例，$1 ≤ a < b ≤ 10^{18}$。

## 标签

#归档/📦/数学

## 解题思路

%%

这是一道求最大公约数的题目。我们可以先分析 $gcd(a + k, b + k)$ 尽可能大的情况。由于 $a$ 和 $b$ 是两个不同的正整数，因此当 $k$ 等于 $b - a$ 时，$gcd(a + k, b + k)$ 达到最大值 $b$。所以，我们需要找到最小的 $k$ 使得 $k$ 能被 $b - a$ 整除。

## Java 代码实现

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int a = scan.nextInt();
        int b = scan.nextInt();
        int diff = b - a;
        int k = diff / gcd(diff, a);
        System.out.println(k);
        scan.close();
    }

    private static int gcd(int a, int b) {
        if (b == 0) {
            return a;
        }
        return gcd(b, a % b);
    }
}
```

## 代码解释

1. 我们使用 `Scanner` 类来读取输入的两数 `a` 和 `b`；
2. 计算出 `diff` 作为 `b - a` 的差值；
3. 调用 `gcd` 函数计算 `diff` 和 `a` 的最大公约数，并用 `diff` 除以这个最大公约数，得到最小的 `k`；
4. 输出 `k` 作为结果。

## 复杂度分析

这里的 `gcd` 函数使用的是欧几里得算法，时间复杂度为 $O(\log \min(a, b))$。由于输入数据范围在 $10^{18}$ 以内，因此时间复杂度可以接受。空间复杂度主要取决于输入数据的大小和 `Scanner` 类，为 $O(1)$。 %%
