# pos partical (1-a)

import java.utl.concurrent.Semphore;
class Oueue{
  //An item
init item;
 //semCon initialized with 0 permits
 //to ensure put() excutes first
 static Semphore semCon = new Semphore(0);
 static Semphore semProd = new Semphore(1);

 //To get an item from the buffer
 void get() {
 try {
   //Before the consumer can consumer an item,
   //it must acquire a permit from semCon
   semCon.acqurire();
  } catch(InterruptedException e) {
    System.out.println("Interrupted Exception Caught");
  }
  //Consumer consuming an item
  System.out.println("Consumer consumer item: " + item);
  //After the Consumer consumer an item,
  //it releases semProd to notify the producer
  semProd.release();
}

//To put an item in the buffer
void put(int item) {
  try{
    //Before the produrce can produce an item,
    // it must acquire a permit from semProd
    semProd.acquire();

    } catch (InterruptedException e) {
      System.out.println("Interrupted exception caught");
    }
// Producer producing an item
this.item item;
System.out.println("Producer produced item: " + item);
// After the producer produces the item,
// it releases semCon to notify the consumer
  semCon.release();
  }
}

// Producer class
class Producer implements Runnable {
Queue q;
Producer (Queue q) {
  this.q = q;
  new Thread(this, " Producer").start();
}
public void run() {
  for (int i=0; i<5; i++)
  //Producer put items
    q.put(i);
  }
}
//Consumer class
class Consumer implements Runnable {
Queue q;
Consumer (Queue q) {
  this.q = q;
  new Thread(this, "Consumer ").start();
}
public void run() {
 for (int i=0; i<5; i++)
  // Consumer put items
    q.get();
  }
}
class prac5 {
  public static void main(String args[]) {
   //creating buffer queue
   Queue q = new Queue();
   //Starting consumer thread
   new Consumer(q);
   //Starting producer thread
   new product(q);
  }
}
    

   
 
