
## ✅ **IB Computer Science – Paper 2 Style Exam Question**
### **Topic: OOP, Linked Lists, Stacks, and Data Structure Selection**

---
### Part A
### **Question 1 – Customer Discount Correction System**
**[Total: 17 marks]**

A retail store uses a transaction system to record each customer's purchase at checkout. Each customer has a name, purchase amount, loyalty tier, and the hour of purchase (in 24-hour format). The store operates from 9:00 AM to 9:00 PM (21:00).

Due to a software bug, a **flat 5% discount** was mistakenly applied to all customers during the **last hour of operation (20:00–21:00)**. The correct discount policy is based on loyalty:

- **Bronze**: 5%
- **Silver**: 10%
- **Gold**: 25%

The system currently stores customers in a **singly linked list** in the order they checked out.

---

### **Given Classes:**

```java
class Customer {
    private String name;
    private double lastPurchase;  // already reduced by 5% due to bug
    private String loyaltyTier;   // "Bronze", "Silver", "Gold"
    private int hour;             // 9 to 21 (24-hour format)

    public Customer(String name, double lastPurchase, String loyaltyTier, int hour) {
        this.name = name;
        this.lastPurchase = lastPurchase;
        this.loyaltyTier = loyaltyTier;
        this.hour = hour;
    }

    // Getters
    public String getName() { return name; }
    public double getLastPurchase() { return lastPurchase; }
    public String getLoyaltyTier() { return loyaltyTier; }
    public int getHour() { return hour; }

    // Setter
    public void setLastPurchase(double amount) { this.lastPurchase = amount; }

    // Returns correct discount rate
    public double getCorrectDiscountRate() {
        switch(loyaltyTier) {
            case "Gold": return 0.25;
            case "Silver": return 0.10;
            case "Bronze": return 0.05;
            default: return 0.05;
        }
    }
}
```

```java
class TransactionLog {
    private Node head;

    private class Node {
        Customer customer;
        Node next;

        public Node(Customer customer) {
            this.customer = customer;
            this.next = null;
        }
    }

    public TransactionLog() {
        head = null;
    }

    // Adds customer to the end of the list (chronological order)
    public void addCustomer(Customer customer) {
        Node newNode = new Node(customer);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }
}
```

---

### **(a)**
Write a method in the `TransactionLog` class called:
```java
public void correctLastHourDiscounts() {
    Customer curCus = new Customer;
    curCus = this.head;
    while (curCus != null){
        if (curCus.getHour() >= 20 && curCus.getHour() <= 21){
            double lTier = curCus.getCorrectDiscountRate();
            double originalPrice = curCus.getLastPurchase() / 0.95;
            curCus.setLastPurchase(originalPrice * (1 - lTier));
        }
        curCus = curCus.next;
    }
    
    
}
```
This method must:
- Traverse the **entire linked list**
- Identify customers who checked out between **20:00 and 21:00 (inclusive)**
- For each such customer:
    - **Reverse the incorrect 5% discount**
    - Apply the **correct discount** based on loyalty tier
    - Update the `lastPurchase` with the corrected value


**[8 marks]**

---

### **(b)**
Explain why using a **singly linked list** is **inefficient** for this type of operation — especially if the store needs to **frequently correct the most recent transactions**.

Suggest a **better data structure** for storing transactions when **recent entries need to be accessed or modified quickly**, and justify your choice.

**[4 marks]**

ANSWER:
In order to get the "most recent transactions," using Linked List forces you to traverse through the entire list before
being able to reach the most recent added. This is because you have to start at "head," and having to use .next one by one
until "null" (if not found) or till the entry being looked for. As a result, making linked list an extremely inefficient
collection to use when trying to obtain and correct the most recent transaction. A better data structure to use would be a stack. This is 
because stacks follow a LIFO structure. Therefore, the store can always access the most recent entry as it will always
be at the top of the stack. As a result, the store can easily modify and access if they need to do anything with the most
recent entries.

---

### **(c)**
Describe how the **stack** data structure follows the **LIFO principle**, and explain why this makes it **particularly suitable** for modeling **transaction undo systems** or **rollback operations** in point-of-sale software.

ANSWER:
Stack is a type of collection that follows the LIFO as it stores entries into the back of the list and keeps the most 
recent entries at the top of the list. It perfectly follows the LIFO principle because a Stack follows the "Last In First Out,"
structure. This type of structure makes it particularly suitable for the transaction undo systems or rollback operations
because all of them are related to "reverting" the most recent changes. By using a LIFO structure to store these changes,
the store is able to directly obtain the most frequent changes and easily undo/revert those changes, instead of having to
traverse through the entire Linked-List, making using Stack way more efficient.

**[3 marks]**

---

### **(d)**
State **one disadvantage** of using a stack for this transaction system if the store also needs to **generate daily reports sorted by time** or **search for a customer by name**.

**[2 marks]**

ANSWER:
Since Stack follow a LIFO structure, it is impossible to obtain and inquire about entries that are in the middle or 
even in the end of the stack. Therefore, if the store needs to track items in a sorted order or search for anything,
it may be extremely inefficient as they will have to do the searching process every single time as they cannot directly 
access using an index. Moreover, the worst case is that the entry they are looking for are always the "first pushed," 
making it the last one to be accessed... following a O(n) time complexity when just trying to search for something before
they can sort.

---



### **Task 1 (c): Binary Search Application**

The store now wants to **quickly find a customer by name** in a **separate sorted array** of customers (not the linked list). The array is sorted alphabetically by name.

Write a **binary search method** (not in the list class) that searches for a customer by name and returns the index, or -1 if not found.

Assume you are given:
```java
Customer[] sortedCustomers; // sorted by name
```

Write the method:
```java
public int binarySearchCustomer(Customer[] arr, String targetName){
    int min = 0;
    int max = arr.length - 1;
    while(min <= max){
        int mid = (min + max) / 2;
        if(arr[mid].getName().compareTo(targetName) < 0){
            max = mid;
            continue;
        }
        if(arr[mid].getName().compareTo(targetName) > 0){
            min = max;
            continue;
        }
        return mid;
        }
    return -1;
    
    
}
```

You may assume `Customer` has a `getName()` method.

**[6 marks]**

> 🔎 *Note: This tests understanding of binary search preconditions (sorted data) and implementation.*

---

## **Question 2: Stack Applications**

### **Standard Stack Operation**

You are given a **stack of integers**. Write a method that **reverses the stack** using **only one queue** as auxiliary storage.

You may only use standard stack and queue operations (`push`, `pop`, `peek`, `enqueue`, `dequeue`, `isEmpty`).

Write the method:
```java
public void reverseStack(Stack<Integer> stack){
    Queue<Integer> q1 = new LinkedList();
    while(!stack.isEmpty()){
        q1.enqueue(stack.pop());
        }
    while(!q1.isEmpty()){
        stack.push(q1.dequeue());
        }
}
```

**[6 marks]**



> 💡 *Hint: Use the queue to temporarily store elements, then re-push them back.*

---