---
title: 快速排序法
tags:
  - c++
id: 1075
categories:
  - 代码
date: 2018-02-17 23:38:41
---
```cpp
    /*************************************************************************
        &gt; File Name: test.cpp
        &gt; Author: 
        &gt; Mail: 
        &gt; Created Time: 2018年02月17日 星期六 23时23分43秒
     ************************************************************************/

    #include&lt;iostream&gt;
    using namespace std;

    void quickSort(int *a, int l, int r) {
      if(l &lt; r) {
        int i, j, x;
        i = l;
        j = r;
        x = a[i];
        while (i &lt; j) {
          while (a[j] &gt; x) {
            j--;
          }
          if (i &lt; j) {
            a[i] = a[j];
            i++;
          }
          while (i &lt; j &amp;&amp; a[i] &lt;x) {
            i++;
          }
          if (i &lt; j) {
            a[j] = a[i];
            j--;
          }
        }
        a[i] = x;
        quickSort(a, l, i-1);
        quickSort(a, i+1, r);
      }
    }

    int main() {
      int a[] = {60, 40, 43, 46, 10,99};
      quickSort(a, 0, 5);
      for (int i = 0; i &lt; 6; i++) {
        cout &lt;&lt; a[i] &lt;&lt; " ";
      }
      cout &lt;&lt; endl;
      return 0;
    }
    ```