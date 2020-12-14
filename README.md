# lab13

>本节目标：
>
>1. 学习强化指针的使用。
>2. 了解指针与数组的关系

获取及提交lab
-------
获取：通过 https://github.com/C-FUDAN-2020/lab13 获取。

提交物：将你完成思考题的文档，编程题的代码作为 lab13 的提交物。

提交：按照要求提交至超星学习通对应的作业题目中。

截止时间：北京时间 2020年12月20日 23:59:59

## 思考题

> 请提交书面答案的文档

#### 1. 指针的使用
学习了指针的小明同学，跃跃欲试。他想用指针而不是数组解决实际问题，因为这样看起来很酷（~~助教也觉得的确很酷~~）。他现在需要解决如下题目：

> 输入：数组的长度和数组每个元素的值（数组长度和数组元素都可以使用int进行存储）

> 输出：排序前后对应位置元素的乘积和    

示例1

> 输入：count=5, elements=2 4 3 5 1

> 输出： 44

> 解释：排序后 1 2 3 4 5，对应乘积和 2 * 1 + 4 * 2 + 3 * 3 + 5 * 4 + 1 * 5 = 44

机智小明很快写下了如下代码。但这个代码有3个bug，请帮他找到，并提供解决方法（同类型bug算一个）。

```c
#include <stdio.h>
int* sort(int*);

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
#### 2. 指针与数组
> &emsp;&emsp;孔乙己等了许久，很恳切的说道，“不能写罢？……我教给你，记着！这些字应该记着。将来做掌柜的时候，写账要用。”我暗想我和掌柜的等级还很远呢，而且我们掌柜也从不将茴香豆上账；
> 又好笑，又不耐烦，懒懒的答他道，“谁要你教，不是草头底下一个来回的回字么？”孔乙己显出极高兴的样子，将两个指头的长指甲敲着柜台，点头说，“对呀对呀！……回字有四样写法，你知道么？”
> 我愈不耐烦了，努着嘴走远。孔乙己刚用指甲蘸了酒，想在柜上写字，见我毫不热心，便又叹一口气，显出极惋惜的样子。（~~文题无关~~）

所以大家还记得数组`a[i][j]`的三种等价表示形式吗？
![ppt图片](./ppt.png)

请回答如下代码中提出的三个问题。

```c
#include <stdio.h>

int main(){
    int a[3][4] = {{1,2,3,4},{5,6,7,8},{9,10,11,12}};
    int *b;
    b = a;
    int i, j;

    // question1: i，j 满足什么条件c1为真（不考虑访问越界）
    int c1 = &a[1][j] == b + i;

    // question2: i，j 满足什么条件c2为真（不考虑访问越界）
    int c2 = *(a[i] + j) == *(b + i + j);

    //question3: i，j 满足什么条件c3为真（不考虑访问越界）
    int c3 = *(a + i) + 1 == b + j;
    
    return 0;
}
```

## 编程题（所有题目此次不允许使用string.h中的函数实现）

#### 1. 编写函数 insert(char* s1, char* s2, int pos)实现在字符串s1中的指定位置pos处插入字符串s2（补全如下代码）。

```c
#include <stdio.h>
void insert(char *s1, char *s2, int pos);
int main(){
    char s1[80],s2[80];
    int pos;
    gets(s1);
    gets(s2);
    scanf("%d",&pos);
    insert(s1,s2,pos);
    puts(s1);
    return 0;
}
void insert(char *s1, char *s2, int pos){
    //TODO: 
}
```
示例1
> 输入：s1 = "Happy  Year", s2 = "New", pos=6

> 输出：Happy New Year

> 解释：插入的位置从0开始，s1中的Happy与Year之间有两个空格。

#### 2. 编写函数 int find(char* haystack, char* needle)，给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1（补全如下代码）。

```c
#include <stdio.h>
int main(){
    char s1[80],s2[80];
    gets(s1);
    gets(s2);
    int pos = find(s1,s2);
    if(pos < 0){
        printf("Not found!\n");
    } else {
        printf("The pos is %d\n",pos);
    }
    return 0;
}
int find(char* haystack, char* needle){
    //TODO: 
    return 0;
}
```
示例1
> 输入：haystack = "hello", needle = "ll"

> 输出：2

示例2
> 输入：haystack = "aaaaa", needle = "bba"

> 输出：-1

示例3
> 输入：haystack = "aaaaa", needle = ""

> 输出：0

## 部分资料来源

1. 力扣（LeetCode）https://leetcode-cn.com/


