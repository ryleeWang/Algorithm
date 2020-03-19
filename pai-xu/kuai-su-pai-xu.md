# 快速排序

## 实现方法（一）

划分思想：设置最后一个位置 data\[end\] 为划分标准，用 small 表示比 data\[end\] 小的数的右区间（初始为 start-1）。从前往后找到第一个小于 data\[end\] 的数所在的位置 index，若 small 和 index 不相等则交换两个位置的数（因为此时 small 指向第一个大于等于 data\[end\] 的数，index 指向第一个小于 data\[end\] 的数）。最后将 small 和 end 所指的数互换。

```cpp
int Partition(int data[], int length, int start, int end) {
    if(data == Null || length <= 0 || start < 0 || end >= length)
        throw new std::exception("invalide parameter");
    int index = RandomInRange(start, end);
    Swap(&data[index], &data[end]);
    int small = start - 1;
    for(index = start; index < end; index++) {
        if(data[index] < data[end]) {
            small++;
            if(small != index)
                Swap(&data[small], &data[index]);
        }
    }
    small++;
    Swap(&data[small], &data[end]);
    return small;
}

void QuickSort(int data[], int length, int start, int end) {
    if(start == end) return;
    int index = Partition(data, length, start, end);
    if(index > start)
        QuickSort(data, length, start, index-1);
    if(index < end)
        QuickSort(data, length, index+1, end);
}
```



