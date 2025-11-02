# Min-and-max-heap-using-array
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to heapify a Min-Heap
void minHeapify(vector<int>& heap, int i, int size) {
    int smallest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < size && heap[left] < heap[smallest])
        smallest = left;
    if (right < size && heap[right] < heap[smallest])
        smallest = right;
    if (smallest != i) {
        swap(heap[i], heap[smallest]);
        minHeapify(heap, smallest, size);
    }
}

// Function to build Min-Heap
void buildMinHeap(vector<int>& heap) {
    for (int i = heap.size() / 2 - 1; i >= 0; i--)
        minHeapify(heap, i, heap.size());
}

// Function to heapify a Max-Heap
void maxHeapify(vector<int>& heap, int i, int size) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < size && heap[left] > heap[largest])
        largest = left;
    if (right < size && heap[right] > heap[largest])
        largest = right;
    if (largest != i) {
        swap(heap[i], heap[largest]);
        maxHeapify(heap, largest, size);
    }
}

// Function to build Max-Heap
void buildMaxHeap(vector<int>& heap) {
    for (int i = heap.size() / 2 - 1; i >= 0; i--)
        maxHeapify(heap, i, heap.size());
}

// Function to delete an element from the heap
void deleteElement(vector<int>& heap, int element, bool isMinHeap) {
    int size = heap.size();
    int index = -1;
    for (int i = 0; i < size; i++) {
        if (heap[i] == element) {
            index = i;
            break;
        }
    }

    if (index == -1) {
        cout << "Element not found in the heap.\n";
        return;
    }

    swap(heap[index], heap[size - 1]);
    heap.pop_back();

    if (isMinHeap)
        minHeapify(heap, index, heap.size());
    else
        maxHeapify(heap, index, heap.size());
}

// Function to display the heap
void displayHeap(const vector<int>& heap) {
    for (int i : heap)
        cout << i << " ";
    cout << endl;
}

int main() {
    vector<int> minHeap = {3, 5, 9, 6, 8, 20, 10, 12, 18, 9};
    vector<int> maxHeap = minHeap;

    // Build the heaps
    buildMinHeap(minHeap);
    buildMaxHeap(maxHeap);

    cout << "Min-Heap: ";
    displayHeap(minHeap);

    cout << "Max-Heap: ";
    displayHeap(maxHeap);

    int elementToDelete;
    cout << "Enter the element to delete from the heap: ";
    cin >> elementToDelete;

    // Delete from Min-Heap
    cout << "Deleting from Min-Heap...\n";
    deleteElement(minHeap, elementToDelete, true);
    cout << "Min-Heap after deletion: ";
    displayHeap(minHeap);

    // Delete from Max-Heap
    cout << "Deleting from Max-Heap...\n";
    deleteElement(maxHeap, elementToDelete, false);
    cout << "Max-Heap after deletion: ";
    displayHeap(maxHeap);

    return 0;
}
[11/2, 3:52 PM] Shaik Abdulla: Experiment -3 
Construct a min and max heap using arrays, delete any element and display the content of the heap
