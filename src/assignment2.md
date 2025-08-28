

### **Part B: "Undo System for Text Editor"**

A simple text editor uses a **stack** to support **undo** operations. Every time the user types a word, it is pushed onto the `actionStack`. The editor also supports a **"redo"** feature, but only **immediately after an undo**, and only **once**.

You are to design a system using **two stacks**:
- `actionStack`: stores words typed (most recent on top)
- `redoStack`: stores words that were undone (only one level of redo allowed)

Implement a method:
```java
public String undoLastAction(){
    while(!redoStack.isEmpty()){
        redoStack.pop();
        }
    String undone = actionStack.pop()
    redoStack.push(undone);
    return undone;
}
```
- Pops the last word from `actionStack`
- Pushes it to `redoStack` (only if `redoStack` is empty — no multiple redos)
- Returns the undone word

Also implement:
```java
public String redoLastUndo(){
    if (redoStack.isEmpty()){
        return null;
        }
    String redoWord = redoStack.pop();
    actionStack.push(redoWord);
    return redoWord;
}
```
- Only works if `redoStack` is not empty
- Moves the word back to `actionStack`
- Returns the word, or `null` if redo not possible


```java
import java.util.Stack;

public class TextEditor {
    private Stack<String> actionStack;
    private Stack<String> redoStack;

    public TextEditor() {
        actionStack = new Stack<>();
        redoStack = new Stack<>();
    }

    /**
     * Undo the last action: pop from actionStack, push to redoStack (if empty)
     * @return the undone word, or null if no action to undo
     */
    public String undoLastAction() {
        
    }

    /**
     * Redo the last undone action
     * @return the word restored, or null if redo not possible
     */
    public String redoLastUndo() {
        
    }
}
```

---

**[7 marks]**

> 🎯 *Tests understanding of stack use in real systems and constraints.*

---

## **Question 3: Binary Trees – Diagram-Based Operations**

### **Given**:
A **binary search tree (BST)** with the following nodes inserted in this order:  
**50, 30, 70, 20, 40, 60, 80**

---

### **Part A**:
Draw the **final structure** of the BST after all insertions. Label all nodes.

**[3 marks]**

                50
             /      \
           30        70
         /   \     /    \
       20    40   60     80

---

### **Part B**:
Now perform the following operations **in sequence**, drawing the tree **after each step**:

1. Insert **35**

                    50
                 /      \
               35        70
             /    \     /    \
            30    40   60     80
           /          
         20       

2. Insert **75**

                    50
                 /      \
               35        75
             /    \     /   \
            30    40   70    80
           /          /
          20        60

3. Delete **30** (use standard BST deletion: if two children, replace with **in-order predecessor**)

                50
             /      \
           35        75
         /    \     /   \
        20    40   70    80
                  /
                60
    

4. Delete **70**

                50
             /      \
           35        75
         /    \     /   \
        20    40   60    80



Show the tree after **each** operation.

**[8 marks – 2 each]**

> 📌 *Ensure diagrams are clear, with left/right children correctly positioned.*

---

### **Part C**:
After the final tree, state:
- The **height** of the tree
- Whether it is **balanced**
- One advantage of a **balanced BST** over an unbalanced one

ANSWER:
The height of the tree is 3, it is balanced. One advantage of using BST over a balanced one is the fact that balanced BSTs
ensures a O(log n) time complexity for operations like searching, insertion, removal, etc. This is because a balanced BST
keeps the height difference between subtrees at most, only one.

**[3 marks]**

---

## **Question 4: Vocabulary & Diagram Quiz**

### **Part A: Definitions**
Define the following terms (1 mark each):

1. Node: a fundamental unit of a data structure (like linked list) that contains both a data and one or more pointers that point to another node or null.
2. Singly linked list, a dynamic data structure that utilizes nodes to store a sequence of elements and to traverse through them one by one from head to tail (null).
3. Stack (LIFO), a linear data structure that stores information using nodes, however Stacks follow a Last in First Out structure
where in order to access information from a stack, the user must go through the stack from the end and slowly work the way to the head.
4. Binary search tree (BST), a dynamic data structure composed of nodes and is organized into a hierarchical structure where the
left subtree is always smaller than the right subtree of the collection.
5. Balanced tree, a binary tree in which the left and right subtrees differ in height by at-most only 1. 
6. In-order traversal, in order traversal is used to traverse a tree fully, where the entire left subtree is visited, then the root, then the right subtree.
7. Overflow (in stack context), when trying to push additional item to a stack, but there is no more memory to hold additional data.
8. Head (in linked list), It is often the first node of a linked list

**[8 marks]**

---

### **Part B: Diagram Interpretation**

You are given the following **singly linked list diagram**:

```
[Anna] -> [Bob] -> [Cara] -> null
```

Each node contains a `Customer` object.

1. Label the **head node**. 
[Anna]
2. What is the **successor** of Bob?
[Cara]
3. What happens if the reference from Bob to Cara is lost?
Then Bob points to null but Cara stays somewhere in the memory that is not accessible.
4. Why can't you traverse from Cara to Bob?
This is a singly linked list, meaning there are no pointers in the node pointing backwards. As a result, you are not
able to traverse backward.

**[4 marks]**

---

### **Part C: Tree Type Identification**

Given three tree diagrams (describe them verbally or sketch in exam):

- **Tree A**: All leaves at same level, full at every level ----- Full binary tree
- **Tree B**: Skewed heavily to the left, height = n-1 ----- Skewed (unbalanced tree)
- **Tree C**: Height difference between left and right subtrees ≤ 1 at every node ----- Balanced BST

Identify each as:
- Full binary tree
- Skewed (unbalanced) tree
- Balanced BST

And state which would give **best search performance** and why.

Using Balanced BST would result in the best performance. This is because it follows a time complexity of O(Log(n)). 
With it being a balanced tree, there will never be any skewed-ness, therefore the binary search algorithm will always
eliminate half of the tree in each cycle. Compared to Tree B, since it is heavily skewed left, the worst case it O(n), 
meaning every single node is checked before the correct one. THis is the same for Tree A, as it is mixed. As a result, 
utilizing Tree C would give the best performance due to it's efficiency when using binary search. 




**[5 marks]**

---