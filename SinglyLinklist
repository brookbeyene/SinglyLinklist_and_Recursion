from __future__ import print_function
import unittest

"""
Brook Beyene
05/04/2018
Assignment 1

    Modifications to the original code are:
        - pop_back and pop_front for removing elements from linked list
        - push_front and push_back for adding new element to the linked list
        - length method for tracking the size of the linked list (line 130)
        - find_the_middle for finding the middle linked list (line 138)
        - delete for deleting the requested element out of the linked list 
          (line 155)

        - test cases for finding the middle and deleting are between
          line 228 and 266

    Source of help (as references):
        https://www.learnsteps.com
        https://stackoverflow.com
        https://www.geeksforgeeks.org


"""

''' when run with "-m unittest", the following produces:
    FAILED (failures=9, errors=2)
    your task is to fix the failing tests by implementing the necessary
    methods. '''

'''
    In the following class I created a class which will contain a Node. Node is a object that has a 
    reference and a value in it. def __init__ is a method that will tell us how to identify each node.
    Within init you see value, and a parameter next_node, this is that reference it has linked with it. 
'''
class LinkedList(object):
    class Node(object):
        # pylint: disable=too-few-public-methods
        ''' no need for get or set, we only access the values inside the
            LinkedList class. and really: never have setters. '''

        def __init__(self, value, next_node):
            self.value = value
            self.next_node = next_node

        def __str__(self):
            return str(self.value) + ";"

        def __repr__(self):
            return repr(self.value)

    def __init__(self, initial=None):
        self.front = self.back = self.current = None

        if initial is not None:
            for i in initial:
                self.push_front(i)

    def empty(self):
        return self.back is None

    def __str__(self):
        elem = []
        curr_node = self.front

        while curr_node is not None:
            elem.append(str(curr_node.value))
            curr_node = curr_node.next_node
        return ', '.join(elem[::-1])

    def __repr__(self):
        return 'LinkedList((' + str(self) + '))'

    def __iter__(self):
        self.current = self.front
        return self

    def __next__(self):
        if self.current:
            tmp = self.current.value
            self.current = self.current.next_node
            return tmp
        else:
            raise StopIteration()

    def push_front(self, value):
        new = self.Node(value, self.front)
        self.front = new
        if self.empty():
            self.front = self.back = new
        else:
            self.front = new

    ''' you need to(at least) implement the following three methods'''

    def pop_front(self):

        if self.empty():
            raise RuntimeError('The linkedList is empty')
        pop = self.front.value
        if self.front == self.back:
            self.back = None
        else:
            self.front = self.front.next_node
        return pop

    def push_back(self, value):

        new_line = self.Node(value, None)
        if not self.back:
            self.front = self.back = new_line
        else:
            popped = self.back
            popped.next_node = new_line
            self.back = new_line

    def pop_back(self):

        if self.empty():
            raise RuntimeError('This LinkedList is empty')
        pop = self.back.value
        popped = self.front
        if not self.front.next_node:
            self.back = self.front = None
        else:
            while popped.next_node is not self.back:
                popped = popped.next_node
            self.back = popped
            popped.next_node = None
        return pop

    def length(self):
        current = self.front
        count = 0
        while current:
            count += 1
            current = current.next_node
        return count

    def find_the_middle(self, length):

        middle = self.front
        found = False
        count = 0
        while middle and found is False:
            count += 1
            if count == length / 2:
                found = True
            else:
                middle = middle.next_node
        if middle is None:
            raise RuntimeError("This linkedList is empty")

        return middle

    def delete(self, value):

        to_be_deleted = self.front
        if to_be_deleted.value is value:
            self.front = to_be_deleted.next_node
        while to_be_deleted.next_node:
            if to_be_deleted.next_node.value is value:
                to_be_deleted.next_node = to_be_deleted.next_node.next_node
            else:
                to_be_deleted = to_be_deleted.next_node


''' C-level work '''


class TestEmpty(unittest.TestCase):
    def test(self):
        self.assertTrue(LinkedList().empty())


class TestPushFrontPopBack(unittest.TestCase):
    def test(self):
        linked_list = LinkedList()
        linked_list.push_front(1)
        linked_list.push_front(2)
        linked_list.push_front(3)
        self.assertFalse(linked_list.empty())
        self.assertEqual(linked_list.pop_back(), 1)
        self.assertEqual(linked_list.pop_back(), 2)
        self.assertEqual(linked_list.pop_back(), 3)
        self.assertTrue(linked_list.empty())


class TestPushFrontPopFront(unittest.TestCase):
    def test(self):
        linked_list = LinkedList()
        linked_list.push_front(1)
        linked_list.push_front(2)
        linked_list.push_front(3)
        self.assertEqual(linked_list.pop_front(), 3)
        self.assertEqual(linked_list.pop_front(), 2)
        self.assertEqual(linked_list.pop_front(), 1)
        self.assertTrue(linked_list.empty())


class TestPushBackPopFront(unittest.TestCase):
    def test(self):
        linked_list = LinkedList()
        linked_list.push_back(1)
        linked_list.push_back(2)
        linked_list.push_back(3)
        self.assertFalse(linked_list.empty())
        self.assertEqual(linked_list.pop_front(), 1)
        self.assertEqual(linked_list.pop_front(), 2)
        self.assertEqual(linked_list.pop_front(), 3)
        self.assertTrue(linked_list.empty())


class TestPushBackPopBack(unittest.TestCase):
    def test(self):
        linked_list = LinkedList()
        linked_list.push_back(1)
        linked_list.push_back("foo")
        linked_list.push_back([3, 2, 1])
        self.assertFalse(linked_list.empty())
        self.assertEqual(linked_list.pop_back(), [3, 2, 1])
        self.assertEqual(linked_list.pop_back(), "foo")
        self.assertEqual(linked_list.pop_back(), 1)
        self.assertTrue(linked_list.empty())


''' B-level work '''


class TesstFindTheMiddle(unittest.TestCase):
    def test_one(self):
        linked_list = LinkedList()
        linked_list.push_front(5)
        linked_list.push_front("AB")
        linked_list.push_front(7)
        linked_list.push_front("932")
        linked_list.push_front(9)
        linked_list.push_front(10)
        linked_list.push_back(1)
        linked_list.push_back("z")
        linked_list.push_back("foo")
        linked_list.push_back([3, 2, 1])


class TestDelete(unittest.TestCase):

    def test_two(self):
        linked_list = LinkedList()
        linked_list.push_front(5)
        linked_list.push_front("AB")
        linked_list.push_front(7)
        linked_list.push_front("932")
        linked_list.push_front(9)
        linked_list.push_front(3)
        linked_list.push_front(10)
        linked_list.push_front(1023)
        linked_list.push_back(1)
        linked_list.push_back("z")
        linked_list.push_back("93 B")
        linked_list.push_back("z")
        linked_list.push_back("foo")
        linked_list.push_back([3, 2, 1])

        linked_list.delete("AB")
        linked_list.delete(3)
        linked_list.delete("93 B")


class TestInitialization(unittest.TestCase):
    def test(self):
        linked_list = LinkedList(("one", 2, 3.141592))
        self.assertEqual(linked_list.pop_back(), "one")
        self.assertEqual(linked_list.pop_back(), 2)
        self.assertEqual(linked_list.pop_back(), 3.141592)


class TestStr(unittest.TestCase):
    def test(self):
        linked_list = LinkedList((1, 2, 3))
        self.assertEqual(linked_list.__str__(), '1, 2, 3')


''' A-level work '''


class TestRepr(unittest.TestCase):
    def test(self):
        linked_list = LinkedList((1, 2, 3))
        self.assertEqual(linked_list.__repr__(), 'LinkedList((1, 2, 3))')


class TestErrors(unittest.TestCase):
    def test_pop_front_empty(self):
        self.assertRaises(RuntimeError, lambda: LinkedList().pop_front())

    def test_pop_back_empty(self):
        self.assertRaises(RuntimeError, lambda: LinkedList().pop_back())


''' write some more test cases. '''

''' extra credit.
    - write test cases for and implement a delete(value) method.
    - write test cases for and implement a method that finds the middle
      element with only a single traversal.
'''

''' the following is a demonstration that uses our data structure as a
    stack'''


def fact(number):
    '''"Pretend" to do recursion via a stack and iteration'''

    if number < 0:
        raise ValueError("Less than zero")
    if number == 0 or number == 1:
        return 1

    stack = LinkedList()
    while number > 1:
        stack.push_front(number)
        number -= 1

    result = 1
    while not stack.empty():
        result *= stack.pop_front()

    return result


class TestFactorial(unittest.TestCase):
    def test_less_than_zero(self):
        self.assertRaises(ValueError, lambda: fact(-1))

    def test_zero(self):
        self.assertEqual(fact(0), 1)

    def test_one(self):
        self.assertEqual(fact(1), 1)

    def test_two(self):
        self.assertEqual(fact(2), 2)

    def test_10(self):
        self.assertEqual(fact(10), 10 * 9 * 8 * 7 * 6 * 5 * 4 * 3 * 2 * 1)


if '__main__' == __name__:
    unittest.main()
