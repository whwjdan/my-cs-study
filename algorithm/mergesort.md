~~~java
public class MergeSortExample {

    public static void mergeSort(int[] arr) {
        int[] tmp = new int[arr.length];
        mergeSort(arr, tmp, 0, arr.length - 1, 0);
    }
    
    // start - mid, mid + 1 - end로 영역을 나누고 재귀적으로 반복한다.
    public static void mergeSort(int[] arr, int[] tmp, int start, int end, int depth) {
        printDepth(depth);
        System.out.println("mergeSort(arr, tmp, " + start + ", " + end + ")");
        
        if (start < end) {
            int mid = (start + end) / 2;
            mergeSort(arr, tmp, start, mid, depth + 1);
            mergeSort(arr, tmp, mid + 1, end, depth + 1);
            merge(arr, tmp, start, mid, end, depth);
        }
    }
    
    // 두개의 영역으로 나누고 정렬하면서 병합한다.
    public static void merge(int[] arr, int[] tmp, int start, int mid, int end, int depth) {
        printDepth(depth);
        System.out.println("merge(arr, tmp, " + start + ", " + mid + ", " + end + ")");
        
        for (int i = start; i <= end; i++) {
            tmp[i] = arr[i];
        }

        int part1 = start;
        int part2 = mid + 1;
        int index = start;

        while (part1 <= mid && part2 <= end) {
            if (tmp[part1] <= tmp[part2]) {
                arr[index] = tmp[part1];
                part1++;
            } else {
                arr[index] = tmp[part2];
                part2++;
            }
            index++;
        }

        while (part1 <= mid) {
            arr[index] = tmp[part1];
            part1++;
            index++;
        }
    }

    // 정렬된 배열을 출력하기 위한 함수이다.
    private static void printArray(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            if (i == arr.length - 1) {
                System.out.print(arr[i]);
            } else {
                System.out.print(arr[i] + ", ");
            }
        }
        System.out.println();
    }
    
    // 재귀 호출의 깊이를 표시하기 위한 함수이다.
    private static void printDepth(int depth) {
        for (int i = 0; i < depth; i++) {
            System.out.print("  ");
        }
    }

    public static void main(String[] args) {
        int[] arr = {3, 9, 4, 7, 5, 0, 1, 6, 8, 2};
        System.out.println("Original array:");
        printArray(arr);
        System.out.println("\nExecuting mergeSort:\n");
        System.out.println("Print depth");
        mergeSort(arr);
        System.out.println("\nSorted array:");
        printArray(arr);
    }
}
~~~
