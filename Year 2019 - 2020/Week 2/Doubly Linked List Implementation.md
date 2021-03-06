### Doubly Linked List Implementation

In this exercise, you need to complete the implementation of a class defining a doubly-linked list, DLList, based on the given skeleton code.

This skeleton already contains the implementation of a class Node. Each Node object has an element and a pointer to the next and previous Node. Implementations of methods getNext, getPrevious, setPrevious, getElement and setNext are also provided. You are encouraged to inspect the comments in the definition of this class to understand the structure.

Following the definition of class Node, we have provided you the skeleton of class DLList. You are expected to complete the implementation of this class by completing following methods:

    addFirst
    removeFirst
    addLast
    removeLast
    size
    addAtPosition
    removeFromPosition
    reverse

You can check the comments in the code to see what each method is expected to implement.

IMPORTANT: You are not allowed to add more fields (class variables) to DLList. In an exam setting, your grade would be overridden to 1, if you do add a field to DLList

IMPORTANT: The reverse method should not mutate the original list. It should return a new list. This is enforced by the specification tests.

```java
class DLList {
  class Node {
    // Each node object has these three fields
    private Object element;
    private Node previous;
    private Node next;

    // Constructor: Creates a Node object with element = e, previous = p and next = n
    Node(Object e, Node p, Node n) {
      element = e;
      previous = p;
      next = n;
    }

    // This function gets Object e as input and sets e as the element of the Node
    public void setElement(Object e) {
      element = e;
    }

    // This function returns the element variable of the Node
    public Object getElement() {
      return element;
    }

    // This function gets Node n as input and sets the next variable of the current Node object as n.
    public void setNext(Node n) {
      next = n;
    }

    // This function returns the next Node
    public Node getNext() {
      return next;
    }

    // This function gets Node p as input and sets the previous variable of the current Node object as p.
    public void setPrevious(Node p) {
      previous = p;
    }

    // This function returns the previous Node
    public Node getPrevious() {
      return previous;
    }
  }

  // Each object in DLList has one field head, which points to the starting Node of DLList.
  private Node head;
  // Each object in DLList has one field tail, which points to the final Node of DLList.
  private Node tail;

  /**
   * Constructor: initialises the head and tail fields as null
   */
  public DLList() {
    head = null;
    tail = null;
  }

  /**
   * @return The element in the head Node of the DLL
   */
  public Object getHead() {
    return head.getElement();
  }

  /**
   * @return The element in the tail Node of the DLL
   */
  public Object getTail() {
    return tail.getElement();
  }

  /**
   * Adds element e in a new Node to the head of the list.
   *
   * @param e
   *     The element to add.
   */
  public void addFirst(Object e) {
    Node h = new Node(e, null, head);
    if(head!=null){
      head.setPrevious(h);
      h.setNext(head);
    }
    if(tail==null){
      tail= h;
    }
    head=h;
  }

  /**
   * Remove the first Node in the list and return its element.
   *
   * @return The element of the head Node. If the list is empty, this method returns null.
   */
  public Object removeFirst() {
    if(head == null) return null;
    Node next = head.getNext();
    Object h = getHead();
    if (next != null)
        next.setPrevious(null);
    head = next;
    return h;
  }

  /**
   * Adds element e in a new Node to the tail of the list.
   *
   * @param e
   *     The element to add.
   */
  public void addLast(Object e) {
     Node t = new Node(e, tail, null);
    if(tail!=null){
      tail.setNext(t);
      t.setPrevious(tail);
    }
    if(head==null){
      head= t;
    }
    tail=t;
  }

  /**
   * Remove the last Node in the list and return its element.
   *
   * @return The element of the tail Node. If the list is empty, this method returns null.
   */
  public Object removeLast() {
    if(tail == null) return null;
    Node prev = tail.getPrevious();
    Object t = getTail();
    if (prev != null)
        prev.setNext(null);
    tail = prev;
    return t;
  }

  /**
   * @return the number of Nodes in the list
   */
  public int size() {
    if(head == null) return 0;
    int count =1;
    Node n = head;
    while(n.getNext() != null){
      n = n.getNext();
      count++;
    }
    return count;
  }

  /**
   * Adds element e in a new Node which is inserted at position pos.
   * The list is zero indexed, so the first element in the list corresponds to position 0.
   * This also means that `addAtPosition(0, e)` has the same effect as `addFirst(e)`.
   * If there is no Node in position pos, this method adds it to the last position.
   *
   * @param pos
   *     The position to insert the element at.
   * @param e
   *     The element to add.
   */
  public void addAtPosition(int pos, Object e) {
    int size = size();
    if (pos == 0)
      addFirst(e);
    else if (pos >= size)
      addLast(e);
    else {
      Node node = head.getNext();
      for(int i =1; i != pos; i++) {
        node = node.getNext();
      }
      Node newNode = new Node(e, node.getPrevious(), node);
      node.getPrevious().setNext(newNode);
      node.setPrevious(newNode);
    }
  }

  /**
   * Remove Node at position pos and return its element.
   * The list is zero indexed, so the first element in the list corresponds to position 0.
   * This also means that `removeFromPosition(0)` has the same effect as `removeFirst()`.
   *
   * @param pos
   *     The position to remove the Node from.
   * @return The element of the Node in position pos. If there is no Node in position pos, this method returns null.
   */
  public Object removeFromPosition(int pos) {
     int size = size();
    if (pos == 0)
      return removeFirst();
    else if (pos == size - 1)
      return removeLast();
    else if ( pos > size - 1)
      return null;
    else {
      Node node = head.getNext();
      for(int i =1; i != pos; i++) {
        node = node.getNext();
      }
      Object removed = node.getElement();
      node.getPrevious().setNext(node.getNext());
      node.getNext().setPrevious(node.getPrevious());
      return removed;
    }
  }

  /**
   * @return A new DLL that contains the elements of the current one in reversed order.
   */
  public DLList reverse() {
    DLList newList = new DLList();
    Node n = tail;
    while(n!=null){
      newList.addLast(n.getElement());
      n = n.getPrevious();
    }
    return newList;
  }
}
```

