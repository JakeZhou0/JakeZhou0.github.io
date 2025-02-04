## 题目描述

 知大写字母 A 的 ASCII 码为 65，请问大写字母 L 的 ASCII 码是多少？

## 输入描述

无

## 输出描述

请输出一个整数

## 样例输出

76

## 说明

字母 A 的 ASCII 码为 65，字母 L 在字母 A 后面第 12 个，所以字母 L 的 ASCII 码为 65+12=77

## 相关标签

#回收站/知识盒/📦/单位换算

## 解题思路

这是一道简单的单位换算题。我们知道 ASCII 码中，连续的字母其 ASCII 码也是连续的。所以只需要计算字母 L 比字母 A 多几个，然后加上 A 的 ASCII 码值即可得到 L 的 ASCII 码值。

代码实现：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        // 输入字母 A 和 L
        char a = 'A';
        char l = 'L';
        // 计算字母 L 比字母 A 多几个
        int diff = l - a;
        // 计算字母 L 的 ASCII 码值
        int asciiCode = 65 + diff;
        // 输出结果
        System.out.println(asciiCode);
        scan.close();
    }
}
```

代码解释：

1. 我们首先导入 Scanner 类，用于从控制台读取输入。
2. 在 main 函数中，我们创建了一个 Scanner 对象 scan。
3. 我们使用 char 类型变量 a 和 l 来存储字母 A 和 L。
4. 计算字母 L 比字母 A 多几个，使用公式 `l - a` 得到差值 diff。
5. 计算字母 L 的 ASCII 码值，使用公式 `65 + diff`，65 是字母 A 的 ASCII 码值。
6. 使用 `System.out.println()` 输出结果。
7. 最后关闭输入流。

这道题的关键在于理解 ASCII 码的连续性，以及使用 Java 进行简单的单位换算和计算。
