# Stack-Queue-Query

Nama : Muh Fajar Siddiq <br>
NIM : H071211078 <br>
Kelas : Struktur Data A <br>

**Stack** adalah wadah objek dimana objek dimasukkan dan dikeluarkan berdasarkan prinsip Last-In First-Out (masuk terakhir keluar pertama) (LIFO) <br>
**Queue** adalah wadah objek dimana objek dimasukkan dan dikeluarkan berdasarkan prinsip First-In First-Out (masuk pertama keluar pertama) (FIFO) <br>

## Stack
**Stack** adalah sebuah struktur data berbentuk linier (lurus) yang mengikuti aturan terentu untuk melakukan operasi. <br>
Data yang memiliki struktur stack. tersusun seperti tumpukan. <br> 

Stack mengikuti prinsip LIFO (Last In First Out), yang berarti elemen yang dimasukkan terakhir akan menjadi elemen pertama yang keluar dari urutan data.
# ![image](https://media.geeksforgeeks.org/wp-content/uploads/geek-stack-1.png)<br>

Contoh Query/Kode dari Stack :

```java
import java.util.*;
public class ArrayStack < E > {

    public static final int CAPACITY = 1000; // default array capacity
    private int topIndex; // index of the top element in stack
    private E[] data; // generic array used for storage
    

    public ArrayStack() {
        this(CAPACITY);
    } // constructs stack with default capacity

    public ArrayStack(int capacity) { // constructs stack with given capacity
        topIndex = -1;
        data = (E[]) new Object[capacity]; // safe cast; compiler may give warning
    }

    public int size() {
        return (topIndex + 1);
    }

    public boolean empty() {
        return (topIndex == -1);
    }

    public void push(E e) throws IllegalStateException {
        if (size() == data.length) throw new IllegalStateException("Stack is full");
        data[++topIndex] = e; // increment topIndex before storing new item
    }

    public E peek() throws EmptyStackException {
        if (empty()) throw new EmptyStackException();
        return data[topIndex];
    }

    public E pop() throws EmptyStackException {
        if (empty()) throw new EmptyStackException();
        E answer = data[topIndex];
        data[topIndex] = null; // dereference to help garbage collection
        topIndex--;
        return answer;
    }

    public static void main(String args[]) {
        ArrayStack < Integer > mystack = new ArrayStack<>();
        mystack.push(9); 
        mystack.push(3); 
        mystack.push(8); 
        System.out.println("Element at the top is :" + mystack.peek()); 
        System.out.println("Element removed is : " + mystack.pop()); 
        System.out.println("The size of the stack is : " + mystack.size()); 
        System.out.println("Element removed is : " + mystack.pop()); 
        System.out.println("Element at the top is : " + mystack.peek());
        mystack.push(10); 
        System.out.println("Stack is empty :  " + mystack.empty()); 
    }
}
```

Dengan output:

```java
Element at the top is :8        
Element removed is : 8          
The size of the stack is : 2    
Element removed is : 3          
Element at the top is : 9        
Stack is empty :  false         
```

## Queue
**Queue** adalah struktur data linier di mana kita dapat menyisipkan dan menghapus elemen data dari ujung belakang (untuk menyisipkan) dan ujung depan (untuk penghapusan). <br>

Struktur data queue menggunakan prinsip FIFO (First In First Out), yang berarti elemen yang dimasukkan pertama kali dari ujung belakang akan menjadi elemen pertama yang dihapus dari ujung depan. <br>

Adapun istilah" dalam queue, yakni operasi **enqueue** (teknik penyisipan) dan **dequeue** (teknik penghapusan). <br>
# ![image](https://media.geeksforgeeks.org/wp-content/uploads/geek-queue-1.png)

Contoh kode queue:
```java
import java.util.*;
public class ArrayQueue < E > {
    private E[] data; // generic array used for storage
    // constructors
    private int frontIndex;
    private int queueSize;

    public ArrayQueue(int capacity) { // constructs queue with given capacity
        data = (E[]) new Object[capacity]; // safe cast; compiler may give warning
        queueSize = 0; // current number of elements
        frontIndex = 0; // index of the front element
        
        
    }
    public ArrayQueue() {
        this(1000);
    } // constructs queue with default capacity

    // methods
    /* Returns the number of elements in the queue. */
    public int size() {
        return queueSize;
    }

    /* Tests whether the queue is empty. */
    public boolean isEmpty() {
        return (queueSize == 0);
    }

    /* Inserts an element at the rear of the queue. */
    public void enqueue(E e) throws IllegalStateException {
        if (queueSize == data.length) throw new IllegalStateException("Queue is full");
        int avail = (frontIndex + queueSize) % data.length; // use modular arithmetic
        data[avail] = e;
        queueSize++;
    }

    /* Returns, but does not remove, the first element of the queue (null if empty). */
    public E first() throws IllegalStateException {
        if (queueSize == data.length) throw new IllegalStateException("Queue is empty");
        return data[frontIndex];
    }

    /* Removes and returns the first element of the queue (null if empty). */
    public E dequeue() throws IllegalStateException {
        if (queueSize == data.length) throw new IllegalStateException("Queue is empty");
        E answer = data[frontIndex];
        data[frontIndex] = null; // dereference to help garbage collection
        frontIndex = (frontIndex + 1) % data.length;
        queueSize--;
        return answer;
    }

    public static void main(String[] args) {
        ArrayQueue queue = new ArrayQueue();
        queue.enqueue(18); 
        System.out.println("Element at front :  " + queue.first()); 
        System.out.println("Element removed from front : " + queue.dequeue()); 
        System.out.println("Queue is Empty : " + queue.isEmpty()); 
        queue.enqueue(79); 
        queue.enqueue(90); 
        System.out.println("Size of the queue : " + queue.size()); 
        System.out.println("Element removed from front end : " + queue.dequeue());
    }
}
```

Dengan output:
```java
Element at front :  18                
Element removed from front : 18       
Queue is Empty : true                
Size of the queue : 2                 
Element removed from front end : 79   
```

Referensi :
- https://tekno.kompas.com/read/2022/12/01/02150047/pengertian-stack-dan-queue-serta-contoh-penerapannya?page=all
-  https://www.scaler.com/topics/java/stack-and-queue-in-java/
-  https://www.geeksforgeeks.org/difference-between-stack-and-queue-data-structures/
