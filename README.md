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
```
