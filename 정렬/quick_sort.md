# 퀵 정렬 (Quick Sort)

- 병합 정렬과 유사하게 분할 정복 알고리즘을 이용해서 배열을 정렬한다. 그러나 따로 병합과정이 필요하지 않고, 피벗(Pivot)을 이용해서 배열의 요소들을 2개의 파티션으로 나눌 때 정렬이 진행된다.
- 평균 복잡도 O(nlogn), 최악의 경우 O(n^2)

코드1

```java
public static void quickSort(int[] arr, int left, int right) {
    if (left < right) {
        int pivot = left;
        int i = left + 1;
        int j = right;
        
        while(i <= j) {
            while(i <= right && arr[i] <= arr[pivot]) i++;
            while(j >= left && arr[j] > arr[pivot]) j--;
            
            if (i < j) swap(arr, i, j);
        }
        
        swap(arr, pivot, j);
        quickSort(arr, left, j - 1);
        quickSort(arr, j + 1, right);
    }
}
```

정렬하려는 배열의 첫번째 원소를 피벗으로 설정하여 정렬한다.

코드2

```java
public static void quickSort(int[] arr, int left, int right) {
    if (left < right) {
        int pivotIndex = (left + right) / 2;
        int pivot = arr[pivotIndex];
        
        swap(arr, left, pivotIndex);
        int i = left + 1;
        int j = right;
        
        while(i <= j) {
            while(i <= right && arr[i] <= pivot) i++;
            while(j >= left && arr[j] > pivot) j--;
            
            if (i < j) swap(arr, i, j);
        }
        
        swap(arr, left, j);
        quickSort(arr, left, j - 1);
        quickSort(arr, j + 1, right);
    }
}
```

피벗을 가운데 값으로 설정한 퀵 정렬
