# circulardoublelinkedlist
class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None

class CircularDoublyLinkedList:
    def __init__(self):
        self.head = None

    def insertBegin(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            new_node.prev = new_node
            new_node.next = new_node
        else:
            new_node.next = self.head
            new_node.prev = self.head.prev
            self.head.prev.next = new_node
            self.head.prev = new_node
            self.head = new_node
        print(f"Inserted {value} at the beginning.")

    def insertEnd(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            new_node.prev = new_node
            new_node.next = new_node
        else:
            new_node.next = self.head
            new_node.prev = self.head.prev
            self.head.prev.next = new_node
            self.head.prev = new_node
        print(f"Inserted {value} at the end.")

    def deleteBegin(self):
        if self.head is None:
            print("List is empty.")
            return
        temp = self.head
        if temp.next == temp:
            self.head = None
        else:
            temp.next.prev = temp.prev
            temp.prev.next = temp.next
            self.head = temp.next
        print("Deleted the first node.")

    def deleteEnd(self):
        if self.head is None:
            print("List is empty.")
            return
        temp = self.head.prev
        if temp.prev == temp:
            self.head = None
        else:
            temp.prev.next = self.head
            self.head.prev = temp.prev
        print("Deleted the last node.")

    def displayList(self):
        if self.head is None:
            print("List is empty.")
            return
        temp = self.head
        print("List:", end=" ")
        while True:
            print(temp.data, end=" ")
            temp = temp.next
            if temp == self.head:
                break
        print()

    def searchElement(self, value):
        if self.head is None:
            print("List is empty.")
            return
        temp = self.head
        position = 1
        while True:
            if temp.data == value:
                print(f"{value} found at position {position}.")
                return
            temp = temp.next
            position += 1
            if temp == self.head:
                break
        print(f"{value} not found in the list.")

if __name__ == "__main__":
    circular_doubly_linked_list = CircularDoublyLinkedList()
    
    while True:
        print("\nCircular Doubly Linked List Operations")
        print("1. Insert at beginning")
        print("2. Insert at end")
        print("3. Delete from beginning")
        print("4. Delete from end")
        print("5. Display list")
        print("6. Search for an element")
        print("7. Exit")
        
        choice = int(input("Enter your choice: "))
        
        if choice == 1:
            value = int(input("Enter value to insert: "))
            circular_doubly_linked_list.insertBegin(value)
        elif choice == 2:
            value = int(input("Enter value to insert: "))
            circular_doubly_linked_list.insertEnd(value)
        elif choice == 3:
            circular_doubly_linked_list.deleteBegin()
        elif choice == 4:
            circular_doubly_linked_list.deleteEnd()
        elif choice == 5:
            circular_doubly_linked_list.displayList()
        elif choice == 6:
            value = int(input("Enter element to search: "))
            circular_doubly_linked_list.searchElement(value)
        elif choice == 7:
            break
        else:
            print("Invalid choice.")
