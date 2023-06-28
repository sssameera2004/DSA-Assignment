METHOD 1:-
class Node():
  def __init__(self,data):
     self.data = data
     self.next = None

class Linkedlist():
   def __init__(self):
     self.head = None
    
   def append(self,data):
     new_node = Node(data)
     h = self.head
     if self.head is None:
         self.head = new_node
         return
     else:
         while h.next!=None:
             h = h.next
         h.next = new_node

   def remove_zeros_from_linkedlist(self, head):
     stack = []
     curr = head
     list = []
     while (curr):
         if curr.data >= 0:
             stack.append(curr)
         else:
             temp = curr
             sum = temp.data
             flag = False
             while (len(stack) != 0):
                 temp2 = stack.pop()
                 sum += temp2.data
                 if sum == 0:
                     flag = True
                     list = []
                     break
                 elif sum > 0:
                     list.append(temp2)
             if not flag:
                 if len(list) > 0:
                     for i in range(len(list)):
                         stack.append(list.pop())
                 stack.append(temp)
         curr = curr.next
     return [i.data for i in stack]

if __name__ == "__main__":
 l = Linkedlist()

 l.append(4)
 l.append(6)
 l.append(-10)
 l.append(8)
 l.append(9)
 l.append(10)
 l.append(-19)
 l.append(10)
 l.append(-18)
 l.append(20)
 l.append(25)
 print(l.remove_zeros_from_linkedlist(l.head))


METHOD 2:-
class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeZeroSumSublists(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
QUESTION 2:-
class Node:
  
    # Constructor to initialize the node object
    def __init__(self, data):
        self.data = data
        self.next = None
  
  
class LinkedList:
  
    # Function to initialize head
    def __init__(self):
        self.head = None
  
    def reverse(self, head, k):
        
        if head == None:
          return None
        current = head
        next = None
        prev = None
        count = 0
  
        # Reverse first k nodes of the linked list
        while(current is not None and count < k):
            next = current.next
            current.next = prev
            prev = current
            current = next
            count += 1
  
        # next is now a pointer to (k+1)th node
        # recursively call for the list starting
        # from current. And make rest of the list as
        # next of first node
        if next is not None:
            head.next = self.reverse(next, k)
  
        # prev is new head of the input list
        return prev
  
    # Function to insert a new node at the beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node
  
    # Utility function to print the linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print(temp.data,end=' ')
            temp = temp.next
  
  
# Driver program
llist = LinkedList()
llist.push(9)
llist.push(8)
llist.push(7)
llist.push(6)
llist.push(5)
llist.push(4)
llist.push(3)
llist.push(2)
llist.push(1)
  
print("Given linked list")
llist.printList()
llist.head = llist.reverse(llist.head, 3)
  
print ("\nReversed Linked list")
llist.printList()



QUESTION 3 :-
Merge a linked list into another linked list at alternate positions.
class LinkedList(object):
    def __init__(self):
        self.head = None
          
    def push(self, new_data:int):
        new_node = Node(new_data)
        new_node.next = self.head
        # 4. Move the head to point to new Node
        self.head = new_node
          
    # Function to print linked list from the Head
    def printList(self):
        temp = self.head
        while temp != None:
            print(temp.data)
            temp = temp.next
      def merge(self, p, q):
        p_curr = p.head
        q_curr = q.head
  
        # swap their positions until one finishes off
        while p_curr != None and q_curr != None:
  
            # Save next pointers
            p_next = p_curr.next
            q_next = q_curr.next
  
            # make q_curr as next of p_curr
            q_curr.next = p_next  # change next pointer of q_curr
            p_curr.next = q_curr  # change next pointer of p_curr
  
            # update current pointers for next iteration
            p_curr = p_next
            q_curr = q_next
            q.head = q_curr
  
  
  
# Driver program to test above functions
llist1 = LinkedList()
llist2 = LinkedList()
  
# Creating LLs
  
# 1.
llist1.push(3)
llist1.push(2)
llist1.push(1)
llist1.push(0)
  
# 2.
for i in range(8, 3, -1):
    llist2.push(i)
  
print("First Linked List:")
llist1.printList()
  
print("Second Linked List:")
llist2.printList()
  
# Merging the LLs
llist1.merge(p=llist1, q=llist2)
  
print("Modified first linked list:")
llist1.printList()
  
print("Modified second linked list:")
llist2.printList()

METHOD 2
class Node:
    def __init__(self, data=None, next=None):
        self.data = data
        self.next = next
 
 
# Helper function to print a given linked list
def printList(msg, head):
 
    print(msg, end='')
 
    ptr = head
    while ptr:
        print(ptr.data, end=' —> ')
        ptr = ptr.next
 
    print('None')
 
 
# Function to construct a linked list by merging alternate nodes of
# two given linked lists using a dummy node
def shuffleMerge(a, b):
 
    dummy = Node()
    tail = dummy
 
    while True:
        # empty list cases
        if a is None:
            tail.next = b
            break
 
        elif b is None:
            tail.next = a
            break
 
        # common case: move two nodes to the tail
        else:
            tail.next = a
            tail = a
            a = a.next
 
            tail.next = b
            tail = b
            b = b.next
 
    return dummy.next
 
 
if __name__ == '__main__':
 
    a = b = None
    for i in reversed(range(1, 8, 2)):
        a = Node(i, a)
 
    for i in reversed(range(2, 7, 2)):
        b = Node(i, b)
 
    # print both lists
    printList('First List: ', a)
    printList('Second List: ', b)
 
    head = shuffleMerge(a, b)
    printList('After Merge: ', head)



