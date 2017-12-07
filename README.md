# python_heap
```
class Heap(object):
    """堆是一个完全二叉树

    关于最大堆:
        最大堆中最大元素值出现在根节点(堆顶)
        堆中父元素的值都大于孩子节点


    关于堆排序的几种操作:
        最大堆调整(maxHeapify): 将堆末端的子节点作调整,使得子节点永远小于父节点
        创建最大堆(buildMaxHeap): 将堆所有数据重新排序，使其成为最大堆
        堆排序(heapSort): 移除第一个数据的根节点，并做最大堆调整的递归运算
    
    从最后一个父节点开发，依次循环到根节点，执行maxHeapify的函数，这样子，根顶元素就是数值最大的
    
    堆排序，就是在buildMaxHeap以后，将根顶元素和最后一个元素交换，并去掉，得到最大的元素，然后重新执行maxHeapify函数
    """

    def __init__(self, array):
        self.array = array

    def maxHeapify(self, array, index, heapSize):
        imax = index

        left = 2 * index + 1
        right = 2 * index + 2

        if left < heapSize and array[index] < array[left]:
            imax = left

        if right < heapSize and array[imax] < array[right]:
            imax = right

        if imax != index:
            array[index], array[imax] = array[imax], array[index]
            self.maxHeapify(array, imax, heapSize)

    def buildMaxHeap(self, array):

        heapSize = len(self.array)

        last_leaf_parent = int((heapSize - 1) / 2)

        for index in range(last_leaf_parent, -1, -1):
            self.maxHeapify(array, index, heapSize)

    def heapSort(self):
        self.buildMaxHeap(self.array)

        for i in range(len(self.array) - 1, 0, -1):
            self.array[0], self.array[i] = self.array[i], self.array[0]
            self.maxHeapify(self.array, 0, i)
        return self.array

def topK():
    "基于堆排序的topK问题"
    random_list = [x for x in range(1, 100001)]
    random.shuffle(random_list)

    # 取初始的10个
    init_list = random_list[:10]
    """构建10个最小堆
    然后继续从剩下的随机list中，读取元素a
    如果a大于堆顶元素(也就是最小的)，取而代之
    然后重新保持最小堆，知道读取完成
    最后对Init_list排序，就会得到topK的答案
    """
    h = Heap(init_list)
    h.heapSort()
    for a in random_list[10:]:
        if a > init_list[0]:
            init_list[0] = a
            h.heapSort()

    h.heapSort()

    print(init_list)
```
参考文献(http://bubkoo.com/2014/01/14/sort-algorithm/heap-sort/)
