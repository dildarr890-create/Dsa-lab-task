// Task 1: Stack and Queue using Linked List (Java)

class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

// ---------------- Stack (LIFO) ----------------
class LinkedStack {
    private Node top;

    public boolean isEmpty() {
        return top == null;
    }

    public void push(int value) {
        Node n = new Node(value);
        n.next = top;
        top = n;
        System.out.println(value + " pushed to stack");
    }

    public void pop() {
        if (isEmpty()) {
            System.out.println("Stack Underflow");
            return;
        }
        System.out.println(top.data + " popped from stack");
        top = top.next;
    }

    public void peek() {
        if (isEmpty()) System.out.println("Stack is empty");
        else System.out.println("Top element: " + top.data);
    }

    public void display() {
        if (isEmpty()) {
            System.out.println("Stack is empty");
            return;
        }
        System.out.print("Stack (top -> bottom): ");
        for (Node t = top; t != null; t = t.next) System.out.print(t.data + " ");
        System.out.println();
    }
}

// ---------------- Queue (FIFO) ----------------
class LinkedQueue {
    private Node front, rear;

    public boolean isEmpty() {
        return front == null;
    }

    public void enqueue(int value) {
        Node n = new Node(value);
        if (rear == null) {
            front = rear = n;
        } else {
            rear.next = n;
            rear = n;
        }
        System.out.println(value + " enqueued");
    }

    public void dequeue() {
        if (isEmpty()) {
            System.out.println("Queue Underflow");
            return;
        }
        System.out.println(front.data + " dequeued");
        front = front.next;
        if (front == null) rear = null;
    }

    public void peek() {
        if (isEmpty()) System.out.println("Queue is empty");
        else System.out.println("Front element: " + front.data);
    }

    public void display() {
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return;
        }
        System.out.print("Queue (front -> rear): ");
        for (Node t = front; t != null; t = t.next) System.out.print(t.data + " ");
        System.out.println();
    }
}

public class StackQueueLinkedList {
    public static void main(String[] args) {
        System.out.println("===== STACK using Linked List =====");
        LinkedStack s = new LinkedStack();
        s.push(10);
        s.push(20);
        s.push(30);
        s.display();
        s.peek();
        s.pop();
        s.display();

        System.out.println("\n===== QUEUE using Linked List =====");
        LinkedQueue q = new LinkedQueue();
        q.enqueue(1);
        q.enqueue(2);
        q.enqueue(3);
        q.display();
        q.peek();
        q.dequeue();
        q.display();
    }
}

// Task 2: 2D Array and Circular Queue using Array (Java)
import java.util.Scanner;

// ---------------- Circular Queue ----------------
class CircularQueue {
    private int[] arr;
    private int front, rear, count, capacity;

    public CircularQueue(int size) {
        capacity = size;
        arr = new int[capacity];
        front = 0;
        rear = -1;
        count = 0;
    }

    public boolean isFull() {
        return count == capacity;
    }

    public boolean isEmpty() {
        return count == 0;
    }

    public void enqueue(int value) {
        if (isFull()) {
            System.out.println("Queue Overflow");
            return;
        }
        rear = (rear + 1) % capacity;
        arr[rear] = value;
        count++;
        System.out.println(value + " enqueued");
    }

    public void dequeue() {
        if (isEmpty()) {
            System.out.println("Queue Underflow");
            return;
        }
        System.out.println(arr[front] + " dequeued");
        front = (front + 1) % capacity;
        count--;
    }

    public void peek() {
        if (isEmpty()) System.out.println("Queue is empty");
        else System.out.println("Front element: " + arr[front]);
    }

    public void display() {
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return;
        }
        System.out.print("Queue (front -> rear): ");
        for (int i = 0; i < count; i++)
            System.out.print(arr[(front + i) % capacity] + " ");
        System.out.println();
    }
}

public class ArrayCircularQueue {

    // ---------------- 2D Array ----------------
    static void demo2DArray() {
        Scanner sc = new Scanner(System.in);
        int rows = 3, cols = 3;
        int[][] arr = new int[rows][cols];

        System.out.println("Enter " + (rows * cols) + " elements for the 3x3 matrix:");
        for (int i = 0; i < rows; i++)
            for (int j = 0; j < cols; j++)
                arr[i][j] = sc.nextInt();

        System.out.println("\nMatrix:");
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) System.out.print(arr[i][j] + "\t");
            System.out.println();
        }

        System.out.println("\nTranspose:");
        for (int i = 0; i < cols; i++) {
            for (int j = 0; j < rows; j++) System.out.print(arr[j][i] + "\t");
            System.out.println();
        }

        int sum = 0;
        for (int i = 0; i < rows; i++)
            for (int j = 0; j < cols; j++) sum += arr[i][j];
        System.out.println("\nSum of all elements: " + sum);
    }

    public static void main(String[] args) {
        System.out.println("===== 2D ARRAY =====");
        demo2DArray();

        System.out.println("\n===== CIRCULAR QUEUE (size 5) =====");
        CircularQueue cq = new CircularQueue(5);
        cq.enqueue(10);
        cq.enqueue(20);
        cq.enqueue(30);
        cq.enqueue(40);
        cq.enqueue(50);
        cq.enqueue(60);   // overflow
        cq.display();
        cq.dequeue();
        cq.dequeue();
        cq.enqueue(60);   // wraps around
        cq.enqueue(70);
        cq.display();
        cq.peek();
    }
}


