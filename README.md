# lab13

>本节目标：
>
>1. 学习强化指针的使用。
>2. 了解指针与数组的关系
>3. 回顾include

获取及提交lab
-------
获取：通过 https://github.com/C-FUDAN-2020/lab13 获取。

提交物：将你完成思考题的文档，编程题的代码作为 lab13 的提交物。

提交：按照要求提交至超星学习通对应的作业题目中。

截止时间：北京时间 2020年12月20日 23:59:59

## 思考题目

> 请提交书面答案的文档

#### 指针的使用
学习了指针的小明同学，跃跃欲试。他想用指针而不是数组解决实际问题，因为这样看起来很酷（助教也觉得的确很酷）。他现在需要解决如下题目：

> 输入：数组的长度和数组每个元素的值（数组长度和数组元素都可以使用int进行存储）

> 输出：排序前后对应位置元素的乘积和    

> 示例如下：

> 5

> 2 4 3 5 1

> 44  // 解释：排序后为 1 2 3 4 5，对应相乘和为 2 * 1 + 4 * 2 + 3 * 3 + 5 * 4 + 1 * 5 = 44

机智小明很快写下了如下代码。但这个代码有3个bug，请帮他找到，并提供解决方法（同类型bug算一个）。

```c
#include <stdio.h>
int * sort(int*);

int main(){
    int count, sum = 0, *arr;
    scanf("%d",&count);
    for(int i = 0; i < count; i++){
        scanf("%d", arr + i);
    }
    int *sorted = sort(arr);
    for(int i = 0; i < count; i++){
        sum += arr[i] * sorted[i];
    }
    printf("%d",sum);
    return 0;
}

int* sort(int* arr){
    int *sorted, len;
    len = sizeof(arr)/sizeof(arr[0]);
    // copy
    for(int i = 0; i < len; i++){
        sorted[i] = arr[i];
    }
    // selection sort
    int min_value, min_pos, temp;
    for(int i = 0; i < len; i++){
        min_value = sorted[i];
        min_pos = i;
        for(int j = i + 1; j < len; j++){
            if(sorted[j] < sorted[i]){
                min_value = sorted[j];
                min_pos = j;
            }
        }
        temp = sorted[i];
        sorted[i] = sorted[min_pos];
        sorted[min_pos] = temp;
    }
    return sorted;
}
```

