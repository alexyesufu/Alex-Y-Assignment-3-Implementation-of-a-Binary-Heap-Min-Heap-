# Alex-Y-Assignment-3-Implementation-of-a-Binary-Heap-Min-Heap-
public class MinHeap {
    private int[] heap;
    private int size;
    private int capacity;

#My code will initialize the MinHeap with a given capacity
    public MinHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        heap = new int[capacity];
    }
#Inserting a new element into the MinHeap
    public void insert(int value) {
        if (size == capacity) {
            System.out.println("Heap is full. Cannot insert more elements.");
            return;
        }

        heap[size] = value;
        heapifyUp(size);
        size++;
    }
#Insert Method to extract my minimum element from the MinHeap
    public int extractMin() {
        if (size == 0) {
            throw new IllegalStateException("Heap is empty. Cannot extract minimum element.");
        }
#Extracting my minimum element (root of the heap)
        int min = heap[0];
        heap[0] = heap[size - 1];
        size--;
        heapifyDown(0);
        return min;
    }
#Method to display the elements of the MinHeap
    public void display() {
        for (int i = 0; i < size; i++) {
            System.out.print(heap[i] + " ");
        }
        System.out.println();
    }

#EXTRA CREDIT:Implement a better visualization for display so that we can see the result better visually. Call this method visualize()

    public void visualize() {
        if (size == 0) {
            System.out.println("Heap is empty.");
            return;
        }

        int height = (int) (Math.log(size) / Math.log(2)) + 1;
        int maxNodes = (int) Math.pow(2, height) - 1;
        int nodesPerLevel = 1;
        int level = 1;
        int count = 0;

        for (int i = 0; i < size; i++) {
            if (count == nodesPerLevel) {
                System.out.println();
                level++;
                nodesPerLevel *= 2;
                count = 0;
            }
            int spaces = (maxNodes / nodesPerLevel) / 2;
            for (int j = 0; j < spaces; j++) {
                System.out.print(" ");
            }
            System.out.print(heap[i]);
            for (int j = 0; j < spaces + 1; j++) {
                System.out.print(" ");
            }
            count++;
        }

        System.out.println();
    }
#To maintain the min heap while inserting a new element

    private void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        if (parentIndex >= 0 && heap[parentIndex] > heap[index]) {
            swap(parentIndex, index);
            heapifyUp(parentIndex);
        }
    }

#To maintain the min heap while extracting the minimum element

    private void heapifyDown(int index) {
        int leftChildIndex = 2 * index + 1;
        int rightChildIndex = 2 * index + 2;
        int smallest = index;

        if (leftChildIndex < size && heap[leftChildIndex] < heap[smallest]) {
            smallest = leftChildIndex;
        }

        if (rightChildIndex < size && heap[rightChildIndex] < heap[smallest]) {
            smallest = rightChildIndex;
        }

        if (smallest != index) {
            swap(smallest, index);
            heapifyDown(smallest);
        }
    }

#Insert Method to swap two elements in my heap
    private void swap(int i, int j) {
        int temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }

    public static void main(String[] args) {
        MinHeap minHeap = new MinHeap(10);

        minHeap.insert(5);
        minHeap.insert(10);
        minHeap.insert(3);
        minHeap.insert(8);
        minHeap.insert(1);

        System.out.println("Heap elements:");
        minHeap.display();

        System.out.println("Heap visualization:");
        minHeap.visualize();

        System.out.println("Extracted min element: " + minHeap.extractMin());
        System.out.println("Heap elements after extraction:");
        minHeap.display();
    }
}




#EXTRA CREDIT:Implement a better visualization for display so that we can see the result better visually. Call this method visualize()
public void visualize() {
    if (size == 0) {
        System.out.println("Heap is empty.");
        return;
    }

    int height = (int) (Math.log(size) / Math.log(2)) + 1;
    int maxNodes = (int) Math.pow(2, height) - 1;
    int nodesPerLevel = 1;
    int level = 1;
    int count = 0;

    for (int i = 0; i < size; i++) {
        if (count == nodesPerLevel) {
            System.out.println();
            level++;
            nodesPerLevel *= 2;
            count = 0;
        }
        int spaces = (maxNodes / nodesPerLevel) / 2;
        for (int j = 0; j < spaces; j++) {
            System.out.print(" ");
        }
        System.out.print(heap[i]);
        for (int j = 0; j < spaces; j++) {
            System.out.print(" ");
        }
        count++;
    }

    System.out.println();
}
