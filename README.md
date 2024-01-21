# Lab-10
MUHAMMAD UMAIR
SE 3RD C 
12370
Q1: Implement a function to serialize and deserialize a binary tree.
def serialize(root):
    if not root:
        return 'None'
    return f'{root.key},{serialize(root.left)},{serialize(root.right)}'

def deserialize(data):
    nodes = data.split(',')

    def build_tree():
        val = nodes.pop(0)
        if val == 'None':
            return None
        node = Node(int(val))
        node.left = build_tree()
        node.right = build_tree()
        return node

    return build_tree()

 Output for Q1: No direct output, as it is a pair of function definitions.

 Q2: Write a function to find the diameter of a binary tree.
def diameter_of_binary_tree(root):
    def height_and_diameter(node):
        if not node:
            return 0, 0
        left_height, left_diameter = height_and_diameter(node.left)
        right_height, right_diameter = height_and_diameter(node.right)

        current_diameter = left_height + right_height
        current_diameter = max(current_diameter, left_diameter, right_diameter)

        return 1 + max(left_height, right_height), current_diameter

    _, diameter = height_and_diameter(root)
    return diameter

Output for Q2: No direct output, as it is a function definition.

 Q3: Implement a function to construct a Huffman tree from a given set of frequencies.
(Assuming frequencies are given as a list of tuples: (character, frequency))
import heapq

class HuffmanNode:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

def construct_huffman_tree(frequencies):
    heap = [HuffmanNode(char, freq) for char, freq in frequencies]
    heapq.heapify(heap)

    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)
        merged = HuffmanNode(None, left.freq + right.freq)
        merged.left, merged.right = left, right
        heapq.heappush(heap, merged)

    return heap[0]

Output for Q3: No direct output, as it is a function definition.

Q4: Implement AVL tree insertion and deletion operations.
# (Assuming AVL tree is already implemented with Node class)

def height(node):
    if not node:
        return 0
    return node.height

def update_height(node):
    if not node:
        return 0
    node.height = 1 + max(height(node.left), height(node.right))
    return node.height

def balance_factor(node):
    if not node:
        return 0
    return height(node.left) - height(node.right)

def rotate_right(y):
    x = y.left
    T2 = x.right

    x.right = y
    y.left = T2

    update_height(y)
    update_height(x)

    return x

def rotate_left(x):
    y = x.right
    T2 = y.left

    y.left = x
    x.right = T2

    update_height(x)
    update_height(y)

    return y

def avl_insert(root, key):
    if not root:
        return Node(key)

    if key < root.key:
        root.left = avl_insert(root.left, key)
    else:
        root.right = avl_insert(root.right, key)

    update_height(root)

    balance = balance_factor(root)

    # Left-Left case
    if balance > 1 and key < root.left.key:
        return rotate_right(root)

    # Right-Right case
    if balance < -1 and key > root.right.key:
        return rotate_left(root)

    # Left-Right case
    if balance > 1 and key > root.left.key:
        root.left = rotate_left(root.left)
        return rotate_right(root)

    # Right-Left case
    if balance < -1 and key < root.right.key:
        root.right = rotate_right(root.right)
        return rotate_left(root)

    return root

def avl_delete(root, key):
    if not root:
        return root

    if key < root.key:
        root.left = avl_delete(root.left, key)
    elif key > root.key:
        root.right = avl_delete(root.right, key)
    else:
        if not root.left:
            return root.right
        elif not root.right:
            return root.left

        temp = find_min(root.right)
        root.key = temp.key
        root.right = avl_delete(root.right, temp.key)

    update_height(root)

    balance = balance_factor(root)

    # Left-Left case
    if balance > 1 and balance_factor(root.left) >= 0:
        return rotate_right(root)

    # Right-Right case
    if balance < -1 and balance_factor(root.right) <= 0:
        return rotate_left(root)

    # Left-Right case
    if balance > 1 and balance_factor(root.left) < 0:
        root.left = rotate_left(root.left)
        return rotate_right(root)

    # Right-Left case
    if balance < -1 and balance_factor(root.right) > 0:
        root.right = rotate_right(root.right)
        return rotate_left(root)

    return root

Output for Q4: No direct output, as it is a set of function definitions.

Q5: Write functions to perform rotations (left and right) in an AVL tree.
# (Rotations are already implemented in AVL tree insert and delete operations)

Output for Q5: No direct output, as rotations are part of the AVL tree operations.
```
