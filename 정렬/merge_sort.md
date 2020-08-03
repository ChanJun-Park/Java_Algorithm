# 병합정렬(Merge Sort)

- 분할 정복을 이용하여 배열에 있는 요소들을 정렬한다.
- O(nlogn)

코드1

```java
public static int[] temp;
public static void mergeSort(int[] arr) {
    if (arr.length == 1) return;
    temp = new int[arr.length];

    merge(arr, 0, arr.length - 1);
}

public static void merge(int[] arr, int begin, int end) {
    if (begin >= end) return;
    
    int mid = (begin + end) / 2;
    merge(arr, begin, mid);
    merge(arr, mid + 1, end);
    
    for (int i = begin; i <= end; i++) {
        temp[i] = arr[i]; 
    }
    
    int i = begin;
    int j = mid + 1;
    int k = begin;
    
    while(i <= mid && j <= end) {
        arr[k++] = temp[i] < temp[j] ? temp[i++] : temp[j++];
    }
    while (i <= mid) arr[k++] = temp[i++];
    while (j <= end) arr[k++] = temp[j++];
    
}
```

강사님 코드. `public static int[] temp;` 처럼 static 한 공간을 만들어줘야 한다. O(n) 크기의 메모리 공간을 한번만 만들어주면 된다.

코드2

```java
public static void mergeSort(int[] a, int n) {
    if (n < 2)
        return;
    int mid = n / 2;
    int[] l = new int[mid];
    int[] r = new int[n - mid];

    for (int i = 0; i < mid; i++) {
        l[i] = a[i];
    }
    for (int i = mid; i < n; i++) {
        r[i - mid] = a[i];
    }
    mergeSort(l, mid);
    mergeSort(r, n - mid);

    merge(a, l, r, mid, n - mid);
}

public static void merge(int[] a, int[] l, int[] r, int left, int right) {

    int i = 0, j = 0, k = 0;

    while (i < left && j < right) {

        if (l[i] <= r[j])
            a[k++] = l[i++];
        else
            a[k++] = r[j++];

    }

    while (i < left)
        a[k++] = l[i++];

    while (j < right)
        a[k++] = r[j++];
}
```

앞선 코드보다 재귀적 동작 해석이 더 자연스럽다. 그러나 O(nlogn) 크기의 메모리 공간이 필요하다.
