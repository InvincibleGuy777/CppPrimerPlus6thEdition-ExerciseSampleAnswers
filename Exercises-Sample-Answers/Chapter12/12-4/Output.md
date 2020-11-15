### OUTPUT 12-4

```
Enter an item to push into the stack (#1): addd
Invalid input! Item must be a long integer!
Enter an item to push into the stack (#1): 12a
item 12 push success.
Enter an item to push into the stack (#2): s23
Invalid input! Item must be a long integer!
Enter an item to push into the stack (#2): 23xc
item 23 push success.
Enter an item to push into the stack (#3): 5x2
item 5 push success.
Enter an item to push into the stack (#4): 23
item 23 push success.
Enter an item to push into the stack (#5): 234
stack #1 is full now.
 push fail~ Loop exit.
copy stack #1 to stack #3:
pop stack #3 until it's empty:
stack #3 pop out item #1: 23
stack #3 pop out item #2: 5
stack #3 pop out item #3: 23
stack #3 pop out item #4: 12
stack #3 has 4 elements in total.

Pop out one element in stack #1

Assign stack #1 to stack #2:
pop stack #2 until it's empty:
stack #2 pop out item #1: 5
stack #2 pop out item #2: 23
stack #2 pop out item #3: 12
stack #2 has 3 elements in total.
Done!

Before stacks destroy: Stack #1 ADDR: 0x62fd20
Stack #2 ADDR: 0x62fd10
Stack #3 ADDR: 0x62fcf0
Now destructors executing:
Stack 0x62fcf0 destroyed~
Stack 0x62fd10 destroyed~
Stack 0x62fd20 destroyed~

```