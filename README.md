import java.util.Stack;

class LinearQueueUsingStack {
    private Stack<Integer> stack1; // For enqueue operation
    private Stack<Integer> stack2; // For dequeue operation

    // Constructor to initialize the stacks
    public LinearQueueUsingStack() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }

    // Check if the queue is empty
    public boolean isEmpty() {
        return (stack1.isEmpty() && stack2.isEmpty());
    }

    // Get the current size of the queue
    public int size() {
        return (stack1.size() + stack2.size());
    }

    // Insert an element at the rear of the queue
    public void enqueue(int item) {
        stack1.push(item);
        System.out.println("Enqueued: " + item);
    }

    // Remove and return the element at the front of the queue
    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. Cannot dequeue element.");
            return -1;
        }

        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }

        int removedItem = stack2.pop();
        System.out.println("Dequeued: " + removedItem);
        return removedItem;
    }

    // Get the element at the front of the queue without removing it
    public int peek() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return -1;
        }

        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }

        return stack2.peek();
    }
}

public class Main {
    public static void main(String[] args) {
        LinearQueueUsingStack queue = new LinearQueueUsingStack();

        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        queue.enqueue(40);
        queue.enqueue(50);

        System.out.println("Queue size: " + queue.size());
        System.out.println("Front of the queue: " + queue.peek());

        queue.dequeue();
        queue.dequeue();
        queue.dequeue();

        System.out.println("Queue size: " + queue.size());
        System.out.println("Front of the queue: " + queue.peek());

        queue.enqueue(60);
        queue.enqueue(70);

        System.out.println("Queue size: " + queue.size());
        System.out.println("Front of the queue: " + queue.peek());
    }
}






class CircularQueue {
    private int maxSize; // maximum size of the queue
    private int[] queueArray; // array to store elements
    private int front; // front of the queue
    private int rear; // rear of the queue
    private int currentSize; // current size of the queue

    // Constructor to initialize the queue
    public CircularQueue(int size) {
        maxSize = size + 1; // Add 1 to account for circular behavior
        queueArray = new int[maxSize];
        front = 0;
        rear = 0;
        currentSize = 0;
    }

    // Check if the queue is empty
    public boolean isEmpty() {
        return (currentSize == 0);
    }

    // Check if the queue is full
    public boolean isFull() {
        return (currentSize == maxSize - 1);
    }

    // Get the current size of the queue
    public int size() {
        return currentSize;
    }

    // Insert an element at the rear of the queue
    public void enqueue(int item) {
        if (isFull()) {
            System.out.println("Queue is full. Cannot enqueue element.");
            return;
        }
        rear = (rear + 1) % maxSize; // Wrap around to the beginning if rear reaches the end
        queueArray[rear] = item;
        currentSize++;
        System.out.println("Enqueued: " + item);
    }

    // Remove and return the element at the front of the queue
    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. Cannot dequeue element.");
            return -1;
        }
        front = (front + 1) % maxSize; // Wrap around to the beginning if front reaches the end
        int removedItem = queueArray[front];
        currentSize--;
        System.out.println("Dequeued: " + removedItem);
        return removedItem;
    }

    // Get the element at the front of the queue without removing it
    public int peek() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return -1;
        }
        int frontIndex = (front + 1) % maxSize; // Calculate the index of the front element
        return queueArray[frontIndex];
    }
}

public class Main {
    public static void main(String[] args) {
        CircularQueue queue = new CircularQueue(5);

        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        queue.enqueue(40);
        queue.enqueue(50);

        System.out.println("Queue size: " + queue.size());
        System.out.println("Front of the queue: " + queue.peek());

        queue.dequeue();
        queue.dequeue();
        queue.dequeue();

        System.out.println("Queue size: " + queue.size());
        System.out.println("Front of the queue: " + queue.peek());

        queue.enqueue(60);
        queue.enqueue(70);

        System.out.println("Queue size: " + queue.size());
        System.out.println("Front of the queue: " + queue.peek());
    }
}
