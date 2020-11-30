### NOTE
See sample answers of `b.` and `c.` in `port_h.md`.

### INPUT EXAMPLE

```
Tawny
-1
a
12as
The Sharp
-VINTAGE-
3
viNtAGE
The Noble
1904
Ruby
8
The Melt
-OLD PARIS-
1
Old Velvet
1865
```

### OUTPUT

```
Enter port's brand: Tawny
Enter port's total bottles: -1
Invalid input, bottles must be a non-negative integer!
Enter port's total bottles: a
Invalid input, bottles must be a non-negative integer!
Enter port's total bottles: 12as
Enter port's kind: The Sharp

Enter port's brand: -VINTAGE-
Enter port's total bottles: 3
Enter port's kind:    viNtAGE
Enter the nickname of vintage port: The Noble
Enter the vintage year of vintage port: 1904

Enter port's brand: Ruby
Enter port's total bottles: 8
Enter port's kind: The Melt

Enter port's brand: -OLD PARIS-
Enter port's total bottles: 1
Enter port's kind: vintage
Enter the nickname of vintage port: Old Velvet
Enter the vintage year of vintage port: 1865

Use of virtual function Show():
  Brand: Tawny
   Kind: The Sharp
Bottles: 12
  Brand: -VINTAGE-
   Kind: vintage
Bottles: 3
NickName: The Noble
    Year: 1904
  Brand: Ruby
   Kind: The Melt
Bottles: 8
  Brand: -OLD PARIS-
   Kind: vintage
Bottles: 1
NickName: Old Velvet
    Year: 1865

Use of operator<<():
Tawny, The Sharp, 12
-VINTAGE-, vintage, 3, The Noble, 1904
Ruby, The Melt, 8
-OLD PARIS-, vintage, 1, Old Velvet, 1865
Done.

```