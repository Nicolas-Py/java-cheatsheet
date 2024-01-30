# How to create Threads

### With Runnable Interface
``` java
public static void example() {
	Thread t1 = new Thread(() -> {
		// override of run() func 
	}); 
	
}

```
### Like a normal Human
``` java
public class MyThread extends Thread {
	private string name;
	public MyThread(String name) {
		this.name = name;
	}
	
	@Override
	public void run(){
	// smth
	}

}

public static void example() {
	Thread t1 = new MyThread("Test"); 
}

```

# Difference run() vs start()
ThreadObj.run() => called die run methode des objektes und führt diese in main thread aus (was keinen fkn sinn macht)

ThreadObj.start() => erstellt einen neuen thread neben den main und führt auf diesen die run Methode aus (parallel zur main was sinn macht)
# Locks

## ReentrantReadWriteLock
The `ReentrantReadWriteLock` in Java is a type of lock that allows multiple threads to read a certain resource simultaneously, but only one thread to write to the resource at any given time. It's an implementation of the `ReadWriteLock` interface introduced in Java to provide a more flexible locking mechanism than the traditional `synchronized` keyword.

Here are the main functions of `ReentrantReadWriteLock`:

1. **Read Locks:**
   - Multiple threads can acquire the read lock simultaneously.
   - Reading can proceed concurrently as long as no threads hold the write lock.

2. **Write Locks:**
   - Only one thread can acquire the write lock at a time.
   - Writing is exclusive, meaning no other threads can hold either the read or write lock while the write lock is held.

3. **Reentrancy:**
   - Similar to `ReentrantLock`, `ReentrantReadWriteLock` supports reentrant behavior. A thread that holds the read lock can acquire it again without blocking, and the same applies to the write lock.

4. **Lock Upgrading:**
   - A thread holding the read lock can attempt to acquire the write lock without releasing the read lock. This is known as lock upgrading.

5. **Lock Downgrading:**
   - A thread holding the write lock can voluntarily release it and acquire the read lock. This is known as lock downgrading.

6. **Fairness:**
   - The `ReentrantReadWriteLock` allows for optional fairness. When fairness is enabled, the lock favors granting access to the longest-waiting thread.

Here is a simple example demonstrating the usage of `ReentrantReadWriteLock`:

```java
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class SharedResource {
    private int data = 0;
    private final ReentrantReadWriteLock lock = new ReentrantReadWriteLock();

    public int readData() {
        lock.readLock().lock();
        try {
            return data;
        } finally {
            lock.readLock().unlock();
        }
    }

    public void writeData(int newData) {
        lock.writeLock().lock();
        try {
            data = newData;
        } finally {
            lock.writeLock().unlock();
        }
    }
}
```

In this example, multiple threads can read `data` concurrently, but only one thread can write to it at a time.
