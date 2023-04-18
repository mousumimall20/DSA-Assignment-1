Q1. Write a program to find all pairs of an integer array whose sum is equal to a given number?

ans:-
def find_pairs_with_sum(arr, target_sum):
   
    pairs = []
    hashmap = {}  # to store the complement of each element in the array

    for num in arr:
        complement = target_sum - num
        if complement in hashmap:
            pairs.append((num, complement))
        hashmap[num] = True

    return pairs

arr = [2, 3, 4, 5, 6, 7, 8, 9]
target_sum = 9
result = find_pairs_with_sum(arr, target_sum)
if result:
    print(f"Pairs with sum {target_sum}: {result}")
else:
    print("No pairs found.")



Q2. Write a program to reverse an array in place? In place means you cannot create a new array. You have to update the original array.

Ans:-
def reverse_array_in_place(arr):
    # Use two pointers, one at the beginning and one at the end of the array
    left = 0
    right = len(arr) - 1

    # Swap elements at left and right pointers and move them towards each other
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]  # Swap elements
        left += 1
        right -= 1

arr = [1, 2, 3, 4, 5]
print("Original array:", arr)
reverse_array_in_place(arr)
print("Reversed array:", arr)

Q3. Write a program to check if two strings are a rotation of each other?

Ans:-

def are_rotations(str1, str2):
    if len(str1) != len(str2):
        return False  # If lengths are not equal, they cannot be rotations
    
    # Concatenate str1 with itself to form a new string
    concatenated = str1 + str1
    
    # Check if str2 is a substring of the concatenated string
    if str2 in concatenated:
        return True
    else:
        return False

str1 = "waterbottle"
str2 = "erbottlewat"
if are_rotations(str1, str2):
    print(str1, "and", str2, "are rotations of each other.")
else:
    print(str1, "and", str2, "are not rotations of each other.")

Q4. Write a program to print the first non-repeated character from a string?
Ans:-
def find_first_non_repeated_char(string):
    char_count = {}
    # Count occurrences of each character in the string
    for char in string:
        if char in char_count:
            char_count[char] += 1
        else:
            char_count[char] = 1

    # Find the first character with count equal to 1
    for char in string:
        if char_count[char] == 1:
            return char

    return None
input_string = "hello"
result = find_first_non_repeated_char(input_string)
if result:
    print("The first non-repeated character in the string is:", result)
else:
    print("No non-repeated characters found in the string.")

Q5. Read about the Tower of Hanoi algorithm. Write a program to implement it.

Ans:-
  def tower_of_hanoi(n, source, auxiliary, target):
   
    if n > 0:
        # Move n-1 disks from source peg to auxiliary peg
        tower_of_hanoi(n - 1, source, target, auxiliary)

        # Move the nth disk from source peg to target peg
        print(f"Move disk {n} from {source} to {target}")

        # Move the n-1 disks from auxiliary peg to target peg
        tower_of_hanoi(n - 1, auxiliary, source, target)

n = 3  # Number of disks
source_peg = "A"
auxiliary_peg = "B"
target_peg = "C"
print(f"Solving Tower of Hanoi with {n} disks...")
tower_of_hanoi(n, source_peg, auxiliary_peg, target_peg)

Q6. Read about infix, prefix, and postfix expressions. Write a program to convert postfix to prefix expression.
ans:-
def postfix_to_prefix(expression):

    stack = []
    operators = set(['+', '-', '*', '/', '^'])

    for char in expression:
        if char not in operators:
            # If character is an operand, push to stack
            stack.append(char)
        else:
            # If character is an operator, pop two operands from stack
            operand1 = stack.pop()
            operand2 = stack.pop()

            # Construct a prefix expression by appending operator and operands
            prefix_expression = char + operand2 + operand1

            # Push the prefix expression back to stack
            stack.append(prefix_expression)
    return stack.pop()

postfix_expr = "35+62/*4-"
prefix_expr = postfix_to_prefix(postfix_expr)
print("Postfix expression:", postfix_expr)
print("Prefix expression:", prefix_expr)


Q7. Write a program to convert prefix expression to infix expression.

Ans:-def prefix_to_infix(expression):
  
     stack = []

    # Iterate through the expression from right to left
    for char in reversed(expression):
        if char.isalnum():
            # If character is an operand, push to stack
            stack.append(char)
        else:
            # If character is an operator, pop two operands from stack
            operand1 = stack.pop()
            operand2 = stack.pop()

            # Construct an infix expression by combining operands and operator
            infix_expression = f"({operand1}{char}{operand2})"

            # Push the infix expression back to stack
            stack.append(infix_expression)

    # The final infix expression is at the top of the stack
    return stack.pop()

prefix_expr = "-+3*5/624"
infix_expr = prefix_to_infix(prefix_expr)
print("Prefix expression:", prefix_expr)
print("Infix expression:", infix_expr)


Q8. Write a program to check if all the brackets are closed in a given code snippet.
Ans:-
def are_brackets_closed(code):
    """
    Function to check if all the brackets are closed in a given code snippet.

    Parameters:
        - code (str): Code snippet

    Returns:
        - bool: True if all brackets are closed, False otherwise
    """
    stack = []
    bracket_map = {')': '(', ']': '[', '}': '{'}

    for char in code:
        if char in bracket_map.values():
            # If character is an opening bracket, push to stack
            stack.append(char)
        elif char in bracket_map.keys():
            # If character is a closing bracket, pop top of stack
            if not stack or bracket_map[char] != stack.pop():
                # If stack is empty or popped bracket does not match
                # with the corresponding opening bracket, return False
                return False

    # If stack is empty, all brackets are closed
    return not stack
code_snippet = "(3 + [5 * {6 - 2}])"
if are_brackets_closed(code_snippet):
    print("All brackets are closed in the code snippet.")
else:
    print("Not all brackets are closed in the code snippet.")

Q9. Write a program to reverse a stack.
Ans:-

def reverse_stack(stack):
    """
    Function to reverse the elements of a stack using recursion.

    Parameters:
        - stack (list): Stack to be reversed

    Returns:
        - None
    """
    if not stack:
        # Base case: if stack is empty, return
        return

    # Remove the top element from the stack
    top_element = stack.pop()

    # Recursively reverse the remaining stack
    reverse_stack(stack)

    # Insert the top element at the bottom of the stack
    insert_at_bottom(stack, top_element)


def insert_at_bottom(stack, item):
    """
    Helper function to insert an item at the bottom of a stack using recursion.

    Parameters:
        - stack (list): Stack to insert the item
        - item (Any): Item to be inserted at the bottom of the stack

    Returns:
        - None
    """
    if not stack:
        # If stack is empty, simply push the item
        stack.append(item)
    else:
        # If stack is not empty, recursively pop and push elements
        # until the stack is empty, then push the item
        temp = stack.pop()
        insert_at_bottom(stack, item)
        stack.append(temp)

stack = [1, 2, 3, 4, 5]
print("Original stack:", stack)
reverse_stack(stack)
print("Reversed stack:", stack)

Q10. Write a program to find the smallest number using a stack.
Ans:-
class Stack:
    """
    Stack class with additional methods to find the smallest element.
    """
    def __init__(self):
        self.items = []
        self.min_stack = []

    def push(self, item):
        self.items.append(item)
        if not self.min_stack or item <= self.min_stack[-1]:
            self.min_stack.append(item)

    def pop(self):
        if not self.items:
            return None
        if self.items[-1] == self.min_stack[-1]:
            self.min_stack.pop()
        return self.items.pop()

    def peek(self):
        if not self.items:
            return None
        return self.items[-1]

    def is_empty(self):
        return not self.items

    def get_min(self):
        if not self.min_stack:
            return None
        return self.min_stack[-1]

stack = Stack()
stack.push(5)
stack.push(3)
stack.push(7)
stack.push(1)
stack.push(9)
print("Original stack:", stack.items)
print("Smallest element:", stack.get_min())
