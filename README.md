# Linkedlist-problems

## Problems 1: Merge k Sorted Lists
```
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.
```

```java
class Node {
      int val;
      Node next;
      Node(int val, Node next) { this.val = val; this.next = next; }
 }
 
class LinkedListProblem {
    Node getMerge(Node l1, Node l2) {
        Node root = null;
        Node curr = root;

        while(l1 != null || l2 != null) {
            Node node = null;
            if (l1 != null && l2 != null) {
                if(l1.val < l2.val) {
                    node  = new Node(l1.val, null);
                    l1 = l1.next;
                } else {
                    node  = new Node(l2.val, null);
                    l2 = l2.next;
                }
            } else if (l1 != null) {
                node  = new Node(l1.val, null);
                l1 = l1.next;
            } else {
                node  = new Node(l2.val, null);
                l2 = l2.next;
            }

            if (root == null) {
                root = node;
            }
            else {
                curr.next = node;
            }
            curr = node;
        }
        return root;
    }
    
    Node mergeKLists(Node[] lists) {
        int l = lists.length;
        Node curr = null;
        if (l>0) {
            curr = lists[0];
        }
        for(int i = 1; i<l; i++) {
           curr =  getMerge(curr, lists[i]);
        }
        return curr;
    }
    void getOutput(Node ans) {
        System.out.print("ans: ");
        Node x = ans;
        while(x != null){
            System.out.print(x.val);
            if (x.next != null) {
              System.out.print("->");
            }
            x = x.next;
        }
    }
    public static void main(String[] args) {
      LinkedListProblem obj = new LinkedListProblem();
      Node root1 = new Node(1, new Node(4, new Node(5, null))); // 1 -> 4 -> 5
      Node root2 = new Node(1, new Node(3, new Node(4, null))); // 1 -> 3 -> 4
      Node root3 = new Node(2, new Node(6, null)); // 2 -> 6
      Node lists[] = new Node[] { root1, root2, root3 };
      Node ans = obj.mergeKLists(lists);
      obj.getOutput(ans); // ans: 1->1->2->3->4->4->5->6
    }
}

```
