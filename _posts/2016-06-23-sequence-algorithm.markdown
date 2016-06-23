---
layout: post
title: 主流排序算法
categories: 技术 算法
tags: 冒泡排序 选择排序 插入排序 归并排序 堆排序 Shell排序 递归
---

### 冒泡排序

**算法描述**

- 假设要从小到大进行排序
- 对于一个元素可比较的序列，从始元素开始，依次比较与之相邻的元素，如果大于后者，则二者位置互换
- 第一次遍历整个序列，最大的元素一定会移动到序列尾
- 第二次遍历整个序列(不包括序列尾元素)，倒数第二大的元素会移动到序列倒数第二的位置
- ...
- 遍历n-1次之后，整个序列排序完毕

**算法动画演示**

![Sortinig bubble sort animation](../image/Sorting_bubblesort_anim.gif)

**算法实现(Java)**

[BubbleSort.java](../src/BubbleSort.java)

    import java.util.Random ;

    public class BubbleSort{

        /*
         * This algorithm is not optimal, because we compare the element which has already ordered
         * when the sequence is ordered, it terminate. We know this from the boolean sorted
         */
        static void bubbleSort(int[] array){
            boolean sorted = false ;
            while(sorted = !sorted){
                for(int i=0; i<array.length-1; i++){
                    if(array[i] > array[i+1]){
                        swap(array, i, i+1) ;
                        sorted = false ;
                    }
                }
            }
        }

        /*
         * This algorithm for bubble sort is optimal, because we will not compare the element which has already ordered
         * The abrove method also can be revised by assign a new variable hi=array.length then hi --
         */
        static void bubbleSortRevised(int[] array, int lo, int hi){
            boolean sorted = false ;
            while(sorted = !sorted){
                for(int i=lo; i<hi-1; i++){
                    if(array[i] > array[i+1]){
                        swap(array, i, i+1) ;
                        sorted = false ;
                    }
                }
                hi -- ;
            }
        }

        /*
         * This is the revised version for method bubbleSort()
         */
        static void bubbleSort2(int[] array){
            boolean sorted = false ;
            int hi = array.length ;
            while(sorted = !sorted){
                for(int i=0; i<hi-1; i++){
                    if(array[i] > array[i+1]){
                        swap(array, i, i+1) ;
                        sorted = false ;
                    }
                }
                hi -- ;
            }
        }

        static void swap(int[] array, int first, int last){
            int temp = array[first] ;
            array[first] = array[last] ;
            array[last] = temp ;
        }

        public static void main(String args[]){
            Random rnd = new Random(26) ;
            int[] array = new int[10] ;
            for(int i=0; i<array.length; i++){
                array[i] = rnd.nextInt(10) ;
            }
            bubbleSort(array) ;
            //bubbleSortRevised(array, 0, array.length) ;
            for(int i : array)
                System.out.print(i + "\t") ;
        }

    }

#### Selection Sort
