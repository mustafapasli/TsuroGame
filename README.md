# TsuroGame
Tsuro Game Implementation in C++

Sample Run Game

- @ubuntu:~/Desktop/$ make
g++ -c -o main.o main.cpp
g++ -std=c++11 -c Card.cpp
g++ -std=c++11 -c Grid.cpp
g++ -std=c++11 -c Player.cpp
g++ -std=c++11 -c Tsuro.cpp
g++ -std=c++11 main.o Card.o Grid.o Player.o Tsuro.o -o exe
- i@ubuntu:~/Desktop$ ./exe
Enter number of player between 2-8>
8
------o--o--------o--o--------Q--o------
|                                      |
|                                      |
o     1x1         1x2         1x3      Y
o                                      S
|                                      |
|                                      |
|                                      |
|                                      |
o     2x1         2x2         2x3      o
R                                      X
|                                      |
|                                      |
|                                      |
|                                      |
T     3x1         3x2         3x3      o
o                                      V
|                                      |
|                                      |
------o--o--------o--Z--------o--o------
Player X's turn>
Player X's cards>
....1..2....  ....1..2....  ....1..2....  
:   8  3   :  :   7  4   :  :   6  4   :  
8   1  2   3  8   5  6   3  8   5  7   3  
7   4  7   4  7   1  2   4  7   3  2   4  
:   5  6   :  :   3  8   :  :   1  8   :  
....6..5....  ....6..5....  ....6..5....  
Select a card>
2
....1..2....
:   7  4   :
8   5  6   3
7   1  2   4
:   3  8   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
R
....7..8....
:   1  5   :
6   3  7   1
5   8  4   2
:   2  6   :
....4..3....
Enter a char for rotate(R,L) or next(N)>
N
Enter a position>
2x3
------o--o--------o--o--------Q--o------
|                                      |
|                                      |
o     1x1         1x2         1x3      Y
o                                      S
|                                      |
|                                      |
|                         ....7..8.... |
|                         :   1  5   : |
o     2x1         2x2     6   3  7   1 o
R                         5   8  4   2 o
|                         :   2  6   : |
|                         ....X..3.... |
|                                      |
|                                      |
T     3x1         3x2         3x3      o
o                                      V
|                                      |
|                                      |
------o--o--------o--Z--------o--o------
...

