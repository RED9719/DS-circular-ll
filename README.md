# DS-circular-ll
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class CircularLinkedList:
    def __init__(self):
        self.head = None

    def traverse(self):
        if not self.head:
            print("List is empty")
            return
        current = self.head
        while True:
            print(current.data, end=" -> ")
            current = current.next
            if current == self.head:
                break
        print(current.data, end=" -> ")
        print(current.data)  # Print the last node again to show the circular nature

    def insert_at_beginning(self, data):
        new_node = Node(data)
        if not self.head:
            new_node.next = new_node
            self.head = new_node
            return
        current = self.head
        while current.next != self.head:
            current = current.next
        current.next = new_node
        new_node.next = self.head
        self.head = new_node

    def insert_at_end(self, data):
        new_node = Node(data)
        if not self.head:
            new_node.next = new_node
            self.head = new_node
            return
        current = self.head
        while current.next != self.head:
            current = current.next
        current.next = new_node
        new_node.next = self.head

    def insert_at_position(self, position, data):
        if position < 0:
            print("Invalid position!")
            return
        new_node = Node(data)
        if position == 0:
            self.insert_at_beginning(data)
            return
        current = self.head
        for _ in range(position - 1):
            if not current.next or current.next == self.head:
                print("Position out of bounds!")
                return
            current = current.next
        new_node.next = current.next
        current.next = new_node

    def delete_from_beginning(self):
        if not self.head:
            print("List is empty!")
            return
        if self.head.next == self.head:
            self.head = None
            return
        last = self.head
        while last.next != self.head:
            last = last.next
        self.head = self.head.next
        last.next = self.head

    def delete_from_end(self):
        if not self.head:
            print("List is empty!")
            return
        if self.head.next == self.head:
            self.head = None
            return
        second_last = self.head
        while second_last.next.next != self.head:
            second_last = second_last.next
        second_last.next = self.head

    def delete_from_position(self, position):
        if position < 0 or not self.head:
            print("Invalid position or list is empty!")
            return
        if position == 0:
            self.delete_from_beginning()
            return
        current = self.head
        for _ in range(position - 1):
            if not current.next or current.next == self.head:
                print("Position out of bounds!")
                return
            current = current.next
        if current.next == self.head:
            print("Position out of bounds!")
            return
        current.next = current.next.next

# Example usage
if __name__ == "__main__":
    cll = CircularLinkedList()
    cll.insert_at_beginning(10)
    cll.insert_at_end(20)
    cll.insert_at_end(30)
    cll.insert_at_position(1, 15)
    print("Circular Linked List after insertion:")
    cll.traverse()

    cll.delete_from_beginning()
    print("\nCircular Linked List after deletion from beginning:")
    cll.traverse()

    cll.delete_from_end()
    print("\nCircular Linked List after deletion from end:")
    cll.traverse()

    cll.delete_from_position(1)
    print("\nCircular Linked List after deletion from position 1:")
    cll.traverse()
