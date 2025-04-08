
- [x] https://leetcode.com/problems/remove-element/description/
- [x] https://leetcode.com/problems/single-number/description/
- [x] https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/
- [ ] https://leetcode.com/problems/two-sum/description/
- [ ] https://leetcode.com/problems/palindrome-number/description/
- [ ] https://leetcode.com/problems/palindrome-number/description/
- [ ] https://leetcode.com/problems/palindrome-number/description/
- [ ] 二分查找 binary search
- [ ] 插排 insertion sort
- [ ] 冒泡 bubble sort
- [ ]  fizzbuzz

linkedList:

```js
class listNode {

constructor(value) {

this.value = value;

this.next = null;

}

}

  

class LinkedList {

constructor() {

this.head = null;

}

  

append(value) {

const newNode = new listNode(value)

if (!this.head) {

this.head = newNode;

return

}

let current = this.head;

while (current.next) {

current = current.next

}

current.next = newNode

}

  

prepend(value) {

const newNode = new listNode(value);

if (!this.head) {

this.head = newNode;

return

}

newNode.next = this.head

this.head = newNode

}

  
  

find(value) {

if (this.head.value === value) return this.head;

let current = this.head

while (current) {

if (current.value === value)

return current

current = current.next

}

}

  

delete(value) {

if (!this.head) return;

let current = this.head

if (current.next && current.next.value !== value) {

current = current.next

}

if (current.next) {

current.next = current.next.next

}

}

  

print() {

let current = this.head;

const values = [];

while (current) {

values.push(current.value)

current = current.next;

}

console.log(values.join("->"))

}

}

  

const list = new LinkedList();

list.append(1)

list.append(2)

list.append(3)

list.prepend(0)

list.print()

console.log(list.find(1))

console.log(list)
```

DoublyLinkedList:

```js
class DoublyListNode {

constructor(value) {

this.value = value;

this.next = null;

this.prev = null;

}

}

  

class DoublyLinkedList {

constructor() {

this.head = null;

this.tail = null;

}

  

append(value) {

const newNode = new DoublyListNode(value);

if (!this.head) {

this.head = this.tail = newNode;

return;

}

this.tail.next = newNode;

newNode.prev = this.tail;

this.tail = newNode;

}

  

prepend(value) {

const newNode = new DoublyListNode(value);

if (!this.head) {

this.head = this.tail = newNode;

return;

}

newNode.next = this.head;

this.head.prev = newNode;

this.head = newNode;

}

  

find(value) {

let current = this.head;

while (current) {

if (current.value === value) return current;

current = current.next;

}

return null;

}

  

delete(value) {

if (!this.head) return;

  

// Case 1: The value to delete is the head

if (this.head.value === value) {

if (this.head === this.tail) {

this.head = this.tail = null;

} else {

this.head = this.head.next;

this.head.prev = null;

}

return;

}

  

let current = this.head;

while (current && current.value !== value) {

current = current.next;

}

  

// Case 2: The value to delete is found

if (current) {

if (current === this.tail) {

this.tail = current.prev;

this.tail.next = null;

} else {

current.prev.next = current.next;

current.next.prev = current.prev;

}

}

}

  

print() {

let current = this.head;

const values = [];

while (current) {

values.push(current.value);

current = current.next;

}

console.log(values.join("<->"));

}

}

  

const doublyList = new DoublyLinkedList();

doublyList.append(1)

doublyList.append(2)

doublyList.print()

console.log(doublyList)
```

Tree:

```js
class TreeNode {
  constructor(value) {
    this.value = value;
    this.children = [];
  }

  addChild(childNode) {
    this.children.push(childNode);
  }

  removeChild(value) {
    this.children = this.children.filter(child => child.value !== value);
  }
}

class Tree {
  constructor() {
    this.root = null;
  }

  setRoot(value) {
    this.root = new TreeNode(value);
  }

  // 用 BFS 查找
  find(value) {
    if (!this.root) return null;
    const queue = [this.root];

    while (queue.length > 0) {
      const node = queue.shift();
      if (node.value === value) return node;

      for (const child of node.children) {
        queue.push(child);
      }
    }

    return null;
  }

  // 添加子节点到指定父节点
  add(value, parentValue) {
    const parent = this.find(parentValue);
    if (!parent) {
      console.log(`Parent node "${parentValue}" not found.`);
      return;
    }
    const newNode = new TreeNode(value);
    parent.addChild(newNode);
  }

  // 删除某个节点（只删除它在父节点下的引用，不删除其后代）
  remove(value) {
    if (!this.root) return;
    if (this.root.value === value) {
      this.root = null; // 删除整个树
      return;
    }

    const queue = [this.root];
    while (queue.length > 0) {
      const node = queue.shift();
      node.removeChild(value);
      queue.push(...node.children);
    }
  }

  // 打印整棵树
  print(node = this.root, indent = 0) {
    if (!node) return;
    console.log(' '.repeat(indent) + node.value);
    for (const child of node.children) {
      this.print(child, indent + 2);
    }
  }
}

// ✅ 示例用法
const tree = new Tree();
tree.setRoot("CEO");
tree.add("CTO", "CEO");
tree.add("CFO", "CEO");
tree.add("Engineer1", "CTO");
tree.add("Engineer2", "CTO");
tree.add("Accountant", "CFO");

tree.print();

```
