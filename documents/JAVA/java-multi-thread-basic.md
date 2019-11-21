# Java Multi-Thread 구현 - Basic

### 1. **Multi-thread** 프로그래밍

- 동시에 여러 개의 Thread가 수행 되는 프로그래밍
- Thread는 각각의 작업공간(context)를 가진다.
- 공유자원이 있는경우 race condition이 발생 
- critical section에 대한 동기화(synchronization)의 구현이 필요하다.
  - critical section에 들어갈 수 있는 thread는 한 번에 하나여야 함
  - critical section에 lock을 걸어서 해결

### 2. 임계영역 (Critical Section)

- 두 개 이상의 Thread가 동시에 접근 하게 되는 리소스
- Critical Section에 동시에 Thread가 접근 하게 되면 실행 결과를 보장 할 수 없다.
- Thread간의 순서를 맞추는 동기화 Syncronization이 필요 하다.

### 3. 동기화 (Synchronization)

- 임계 영역에 여러 Thead가 접근 하는 경우 한 Thread가 수행 하는 동안 공유자원을 lock하여 다른 Thread의 접근을 막는다.

- 동기화를 잘 못 구현 하면 deadlock에 빠 질 수 있다.

-  ---get()---||lock||---release()---

  ------get()------||lock||------release()------

  ---------get()---------||lock||---------release()---------

### 4. Java에서 동기화 구현

Syncronized 수행문과 Syncronized 메서드를 활용 하여 구현



##### 1) Syncronized Method

현재 이 메서드가 속해 있는 객체에 Lock을 건다.

Synchronized 메서드 내에서 다른 synchronized 메서드를 호출 하지 않는다. (deadlock방지를 위해)

```java 
package com.company.thread;

class Bank{
    private int money = 10000;


    public int getMoney() {
        return this.money;
    }

    public synchronized void saveMoney(int save){
        int m = this.getMoney();
        try{
            Thread.sleep(3000);
        }catch(InterruptedException e){
            e.printStackTrace();
        }

        setMoney(m+save);

    }

    private void setMoney(int money) {
        this.money = money;
    }

    public synchronized void minusMoney(int minus){
        int m = this.getMoney();
        try{
            Thread.sleep(200);
        }catch(InterruptedException e){
            e.printStackTrace();
        }

        setMoney(m - minus);
    }

}

class Mia extends  Thread{
    public void run(){
        System.out.println("start save");
        SyncTest.myBank.saveMoney(4000);
        System.out.println("save money: " + SyncTest.myBank.getMoney());
    }
}

class Bam extends  Thread{

    public void run(){
        System.out.println("start minus");
        SyncTest.myBank.minusMoney(1000);
        System.out.println("minus money: " + SyncTest.myBank.getMoney());
    }

}
public class SyncTest {

    public static Bank myBank = new Bank();

    public static void main(String[] args) throws InterruptedException {
        Mia m = new Mia();
        m.start();

        Thread.sleep(200);
        Bam b = new Bam();
        b.start();
    }
}

```

위의 결과 문의 리턴 값은 다음과 같다.

<Return>

start save
start minus
save money: 14000
minus money: 13000

왜냐하면 saveMoney, minusMoney의 method에 각각 Synchronized 함수를 걸어 주었기 때문이다. 그렇기 때문에 minusMoney는 saveMoney가 다 끝날때 까지 수행 되지 않는다.  만약 Synchronized를 걸어 주지 않았다면 아래와 같이 뒤죽박죽인 값이 나올 것이다.

<Return>

start save
start minus
minus money: 9000
save money: 14000



##### 2) Syncronized 수행문

`Synchronized(참조형 수식){}` : 참조형 수식에 해당 되는 객체에 Lock을 건다.

```java 
    public  void saveMoney(int save){
        synchronized (this){
            int m = this.getMoney();
            try{
                Thread.sleep(3000);
            }catch(InterruptedException e){
                e.printStackTrace();
            }

            setMoney(m+save);
        }

    }
    public synchronized void minusMoney(int minus){
        synchronized (this){
            int m = this.getMoney();
            try{
                Thread.sleep(200);
            }catch(InterruptedException e){
                e.printStackTrace();
            }

            setMoney(m+minus);
        }
    }
```

### 5. 교착상태(DEADLOCK)

- 프로세스가 자원을 얻지 못해 다음 처리를 하지 못하는 상태를 의마한다. 시스템적으로 한정된 자원을 여러 곳에서 사용하려 할 때 발생한다.
- Example
  - Process1 이 해당객체에 Lock을 걸고 Process2를 기다리는 상태 에서 Process2는 해당 객체에 Lock을 걸고 Process1을 기다리는 상태 
  - 이때, 서로 원하는 리소스가 상대방에게 할당 되어 있어 두 프로세스는 무한정 서로를 기다리게 되는데 이러한 상태를 DeadLock상태라고 한다

### 6. Wait()/Notify()

##### 1) wait() 

- 리소스가 더 이상 유효하지 않은 경우 리소스가 사용 가능할 때 까지 Thread를 None-runnable상태로 전환
- wait() 상태가 된 thread는 notify()가 호출 될 때 까지 기다린다.

##### 2) notify()

- wait() 하고 있는 thread 중 한 thread를 runnable 한 상태로 깨운다.

##### 3) notifyAll()

- wait()하고 있는 모든 Thread가 runnable한 상태가 되도록 한다. notify()보다 notifyAll()을 사용하기를 권장
- 특정 Thread가 통지를 받도록 제어 할 수 없으므로 모두 깨운 후 scheduler에 CPU를 점유하는 것이 좀 더 공평하다.

```java 
package com.company;

import java.util.ArrayList;

class BamLibrary{
    public ArrayList<String> books = new ArrayList<String>();

    public BamLibrary() {
        books.add("A BOOK");
        books.add("B BOOK");
        books.add("C BOOK");
    }

    public synchronized String lendBook() throws InterruptedException {
        Thread t = Thread.currentThread();
        while (books.size() == 0) {
            //notifyAll로 전체를 깨웠을때 또 자원이 없는 애들이 생길 수 있으므로 while을 걸어 리소스를 할당 못받은 애들은 다시 wait을 걸어준다
            System.out.println(t.getName() + " waiting start");
            wait();
            System.out.println(t.getName() + " waiting end");
        }
        String title = books.remove(0);
        System.out.println(t.getName() + " : "+ title + " lend");
        return title;
    }

    public synchronized void returnBook(String title){
        Thread t = Thread.currentThread();
        books.add(title);
        notifyAll();
        System.out.println(t.getName() + " : "+ title + " return");
    }
}

class Student extends Thread{
    public void run(){
        try{
            String title = LibraryMain.library.lendBook();
            sleep(5000);
            LibraryMain.library.returnBook(title);
        }catch(InterruptedException e){
            e.printStackTrace();
        }
    }
}

public class LibraryMain {

    public static BamLibrary library = new BamLibrary();
    public static void main(String[] args) {

        Student std1 = new Student();
        Student std2 = new Student();
        Student std3 = new Student();
        Student std4 = new Student();
        Student std5 = new Student();
        Student std6 = new Student();

        std1.start();
        std2.start();
        std3.start();
        std4.start();
        std5.start();
        std6.start();

    }
}
```



