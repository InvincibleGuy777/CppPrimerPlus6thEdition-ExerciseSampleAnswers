### INPUT EXAMPLE

```
Gay Lab
18
3
zoom
AssHole
-5
242aa
aas2422
1
MaBaoGuo
1aas
3
hunYuan3D
SHARP_ASS
14
45678aa1
2
dark-green
```

### OUTPUT

```
Enter dma's label: Gay Lab
Enter dma's rating: 18
Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: 3
Enter a style: zoom
ABC(...) object 0x10641e0 created~
hasDMA(...) object 0x10641e0 created~
Enter dma's label: AssHole
Enter dma's rating: -5
Invalid input, rating must be a positive integer!
Enter dma's rating: 242aa
Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: aas2422
Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: 1
ABC(...) object 0x10642b0 created~
baseDMA(...) object 0x10642b0 created~
Enter dma's label: MaBaoGuo
Enter dma's rating: 1aas
Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: 3
Enter a style: hunYuan3D
ABC(...) object 0x1064340 created~
hasDMA(...) object 0x1064340 created~
Enter dma's label: SHARP_ASS
Enter dma's rating: 14
Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: 45678aa1
Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: 2
Enter a color: dark-green
ABC(...) object 0x1064410 created~
lacksDMA(...) object 0x1064410 created~


hasDMA View():
 Label: Gay Lab
Rating:18
 Style: zoom

baseDMA View():
 Label: AssHole
Rating:242

hasDMA View():
 Label: MaBaoGuo
Rating:1
 Style: hunYuan3D

lacksDMA View():
 Label: SHARP_ASS
Rating:14
 Color: dark-green
hasDMA object 0x10641e0 destroyed~
ABC object 0x10641e0 destroyed~
baseDMA object 0x10642b0 destroyed~
ABC object 0x10642b0 destroyed~
hasDMA object 0x1064340 destroyed~
ABC object 0x1064340 destroyed~
lacksDMA object 0x1064410 destroyed~
ABC object 0x1064410 destroyed~
Done.

```