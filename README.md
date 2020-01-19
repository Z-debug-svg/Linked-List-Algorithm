# Linked-List-Algorithm
Some Algorithm On Linked-List




# 1:Reverse a linked list ：

# Iterative Method ：
Given pointer to the head node of a linked list, the task is to reverse the linked list. 
We need to reverse the list by changing links between nodes.
Examples:
Input: Head of following linked list
1->2->3->4->NULL
Output: Linked list should be changed to,
4->3->2->1->NULL
Input: Head of following linked list
1->2->3->4->5->NULL
Output: Linked list should be changed to,
5->4->3->2->1->NULL
Input: NULL
Output: NULL
Input: 1->NULL
Output: 1->NULL


Algorithm :
(1)Initialize three pointers prev as NULL, curr as head and next as NULL.
(2)Iterate trough the linked list. In loop, do following.

// Before changing next of current,
// store next node

next = curr->next

// Now change next of current
// This is where actual reversing happens

curr->next = prev

// Move prev and curr one step forward

prev = curr
curr = next


# Understanding the Code :

// Iterative C program to reverse a linked list 

#include <stdio.h> 
#include <stdlib.h> 
  
/* Link list node */

struct Node { 
    int data; 
    struct Node* next; 
}; 
  
/* Function to reverse the linked list */

static void reverse(struct Node** head_ref) 
{ 
    struct Node* prev = NULL; 
    struct Node* current = *head_ref; 
    struct Node* next = NULL; 
    while (current != NULL) { 
        // Store next 
        next = current->next; 
  
        // Reverse current node's pointer 
        current->next = prev; 
  
        // Move pointers one position ahead. 
        prev = current; 
        current = next; 
    } 
    *head_ref = prev; 
} 
  
/* Function to push a node */

void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 
  
/* Function to print linked list */

void printList(struct Node* head) 
{ 
    struct Node* temp = head; 
    while (temp != NULL) { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
    } 
} 
  
/* Driver program to test above function*/

int main() 
{ 
    /* Start with the empty list */
    
    struct Node* head = NULL; 
  
    push(&head, 20); 
    push(&head, 4); 
    push(&head, 15); 
    push(&head, 85); 
  
    printf("Given linked list\n"); 
    printList(head); 
    reverse(&head); 
    printf("\nReversed Linked list \n"); 
    printList(head); 
    getchar(); 
} 


Output:
Given linked list
85 15 4 20 
Reversed Linked list 
20 4 15 85 

Time Complexity: O(n)
Space Complexity: O(1)



# Recursive Method :

algorithm:
   1) Divide the list in two parts - first node and 
      rest of the linked list.
   2) Call reverse for the rest of the linked list.
   3) Link rest to first.
   4) Fix head pointer

# Understanding the Code :

// Recursive C++ program to reverse 
// a linked list 

#include <iostream> 
using namespace std; 
  
/* Link list node */

struct Node { 
    int data; 
    struct Node* next; 
    Node(int data) 
    { 
        this->data = data; 
        next = NULL; 
    } 
}; 
  
struct LinkedList { 
    Node* head; 
    LinkedList() 
    { 
        head = NULL; 
    } 
  
    Node* reverse(Node* head) 
    { 
        if (head == NULL || head->next == NULL) 
            return head; 
  
        /* reverse the rest list and put  
          the first element at the end */
          
        Node* rest = reverse(head->next); 
        head->next->next = head; 
  
        /* tricky step -- see the diagram */
        
        head->next = NULL; 
  
        /* fix the head pointer */
        
        return rest; 
    } 
  
    /* Function to print linked list */
    
    void print() 
    { 
        struct Node* temp = head; 
        while (temp != NULL) { 
            cout << temp->data << " "; 
            temp = temp->next; 
        } 
    } 
  
    void push(int data) 
    { 
        Node* temp = new Node(data); 
        temp->next = head; 
        head = temp; 
    } 
}; 
  
/* Driver program to test above function*/

int main() 
{ 
    /* Start with the empty list */
    
    LinkedList ll; 
    ll.push(20); 
    ll.push(4); 
    ll.push(15); 
    ll.push(85); 
  
    cout << "Given linked list\n"; 
    ll.print(); 
  
    ll.head = ll.reverse(ll.head); 
  
    cout << "\nReversed Linked list \n"; 
    ll.print(); 
    return 0; 
} 

Time Complexity: O(n)
Space Complexity: O(1)



# A Simpler and Tail Recursive Method :

// A simple and tail recursive C++ program to reverse 
// a linked list 

#include <bits/stdc++.h> 
using namespace std; 
  
struct Node { 
    int data; 
    struct Node* next; 
}; 
  
void reverseUtil(Node* curr, Node* prev, Node** head); 
  
// This function mainly calls reverseUtil() 
// with prev as NULL 

void reverse(Node** head) 
{ 
    if (!head) 
        return; 
    reverseUtil(*head, NULL, head); 
} 
  
// A simple and tail recursive function to reverse 
// a linked list.  prev is passed as NULL initially. 

void reverseUtil(Node* curr, Node* prev, Node** head) 
{ 
    /* If last node mark it head*/
    
    if (!curr->next) { 
        *head = curr; 
  
        /* Update next to prev node */
        
        curr->next = prev; 
        return; 
    } 
  
    /* Save curr->next node for recursive call */
    
    Node* next = curr->next; 
  
    /* and update next ..*/
    
    curr->next = prev; 
  
    reverseUtil(next, curr, head); 
} 
  
// A utility function to create a new node 

Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 
  
// A utility function to print a linked list 

void printlist(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    cout << endl; 
} 
  
// Driver program to test above functions 

int main() 
{ 
    Node* head1 = newNode(1); 
    head1->next = newNode(2); 
    head1->next->next = newNode(3); 
    head1->next->next->next = newNode(4); 
    head1->next->next->next->next = newNode(5); 
    head1->next->next->next->next->next = newNode(6); 
    head1->next->next->next->next->next->next = newNode(7); 
    head1->next->next->next->next->next->next->next = newNode(8); 
    cout << "Given linked list\n"; 
    printlist(head1); 
    reverse(&head1); 
    cout << "\nReversed linked list\n"; 
    printlist(head1); 
    return 0; 
} 

Output:
Given linked list
1 2 3 4 5 6 7 8
Reversed linked list
8 7 6 5 4 3 2 1
