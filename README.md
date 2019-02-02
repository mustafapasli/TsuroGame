# TsuroGame

Tsuro Game Implementation in C++

## Tsuro

 - Read the explanations about the original game (https://en.wikipedia.org/wiki/Tsuro)

## Basic Elements of the Game


### Tokens

- Tokens represent players.
- For the version you are going to implement, tokens will be displayed as single characters.

### Path Cards

- Square cards which have 2 ports on each of their sides and various routing information. 
- You can display a Path card as follows:
    ```console
    ....1..2.... 
    :   8  6   : 
    8   1  5   3 
    7   4  7   4 
    :   2  3   : 
    ....6..5....
    ```

- Here, ports are numbered (1,2,3,4,5,6,7,8).
- Inside, the routing information is presented. For the particular card above:
  - port 8 is connected to port 1 
  - port 7 is connected to port 4 
  - port 6 is connected to port 2 
  - port 5 is connected to port 3
- Connections are not directed.
- A path card can be rotated clockwise or counter-clockwise(repeatedly)


### 2D grid

- This game will be played on a 2D grid.
- Each cell on this grid will either be occupied by a path card or it will be empty. 
- Cards can only be placed in empty cells
- Below is an example of a partially filled 3x3 grid
```console
------o--o--------o--o--------o--o------ 
| ....1..2........7..8....             | 
| :   8  6   ::   1  6   :             | 
o 8   1  5   36   8  7   1             o 
o 7   4  7   45   3  4   2             o 
| :   2  3   ::   2  5   :             | 
| ....6..5........4..3....             |  
| ....3..4....                         | 
| :   4  3   :                         | 
o 2   1  6   5                         o 
o 1   2  5   6                         o 
| :   7  8   :                         | 
| ....8..7....                         | 
| ....1..2........1..2........1..2.... | 
| :   5  6   ::   6  5   ::   8  6   : | 
o 8   4  7   38   3  8   38   1  5   3 o 
o 7   3  8   47   4  7   47   4  7   4 o 
| :   2  1   ::   1  2   ::   2  3   : | 
| ....6..5........6..5........6..5.... | 
------o--o--------o--o--------o--o------
```

- On the sides of the grid 'o's represent exit/entry ports of the game.
- A User token may start at any of the exit/entry ports and exit from any of the ports.
- If the ports of path cards(tiles) collide, they are assumed to be connected. For example, port 3 of the tile 1
(first row, first column) is connected to port 6 of the tile on the right.

## Rules of The Game

- For a general understanding of the game please read the necessary wikipedia articles. You can find more information on other webpages.
- Basically:
  - It is a turn-based game.
  - There are at least 2 players, each one has a token.
  - Game starts randomly. (random entry ports are chosen for each player)
  - Initially, the 2D grid is empty.
  - Each player is given a set of cards(Generally 3 cards.)
  - A turn starts with the player deciding on a card(selecting a card from the set given). If the set of cards
is empty, a new set is requested (how you generate a set is up to you. It has to be flexible for further
modifications. So hide unnecessary details.)
  - Once a card is selected, it is placed in an empty cell on the 2D grid.
  - The token follows the route on the card placed.
  - The objective is to remain on the game.
  
## Sample Run Game

```console 
 
 g++ -c -o main.o main.cpp
 g++ -std=c++11 -c Card.cpp
 g++ -std=c++11 -c Grid.cpp
 g++ -std=c++11 -c Player.cpp
 g++ -std=c++11 -c Tsuro.cpp
 g++ -std=c++11 main.o Card.o Grid.o Player.o Tsuro.o -o exe
 
 -@ubuntu:~/Desktop/$ make
 
 -@ubuntu:~/Desktop$ ./exe
 
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
Player Y's turn>
Player Y's cards>
....1..2....  ....1..2....  ....1..2....  
:   5  7   :  :   7  5   :  :   5  8   :  
8   4  6   3  8   3  8   3  8   2  7   3  
7   2  8   4  7   1  6   4  7   3  6   4  
:   3  1   :  :   4  2   :  :   4  1   :  
....6..5....  ....6..5....  ....6..5....  
Select a card>
2
....1..2....
:   7  5   :
8   3  8   3
7   1  6   4
:   4  2   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
L
....3..4....
:   8  6   :
2   5  2   5
1   7  4   6
:   3  1   :
....8..7....
Enter a char for rotate(R,L) or next(N)>
N
Enter a position>
1x3
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 S
|                         :   3  1   : |
|                         ....8..7.... |
|                         ....7..8.... |
|                         :   1  5   : |
o     2x1         2x2     6   3  7   Q o
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
Player Q lost!
------o--o--------o--o--------o--o------
|                         ....3..S.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
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
Player S lost!
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
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
Player Z's turn>
Player Z's cards>
....1..2....  ....1..2....  ....1..2....  
:   4  8   :  :   7  8   :  :   5  6   :  
8   2  5   3  8   2  4   3  8   7  4   3  
7   6  1   4  7   1  3   4  7   8  3   4  
:   7  3   :  :   5  6   :  :   2  1   :  
....6..5....  ....6..5....  ....6..5....  
Select a card>
3
....1..2....
:   5  6   :
8   7  4   3
7   8  3   4
:   2  1   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
N
Enter a position>
3x2
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
|                         ....7..8.... |
|                         :   1  5   : |
o     2x1         2x2     6   3  7   1 o
R                         5   8  4   2 o
|                         :   2  6   : |
|                         ....X..3.... |
|             ....Z..2....             |
|             :   5  6   :             |
T     3x1     8   7  4   3    3x3      o
o             7   8  3   4             V
|             :   2  1   :             |
|             ....6..5....             |
------o--o--------o--o--------o--o------
Player R's turn>
Player R's cards>
....1..2....  ....1..2....  ....1..2....  
:   6  8   :  :   7  8   :  :   5  4   :  
8   2  5   3  8   2  6   3  8   7  6   3  
7   4  7   4  7   1  5   4  7   8  2   4  
:   1  3   :  :   3  4   :  :   3  1   :  
....6..5....  ....6..5....  ....6..5....  
Select a card>
1
....1..2....
:   6  8   :
8   2  5   3
7   4  7   4
:   1  3   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
N  
Enter a position>
2x1
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
| ....1..2....            ....7..8.... |
| :   6  8   :            :   1  5   : |
o 8   2  5   3    2x2     6   3  7   1 o
o 7   4  7   R            5   8  4   2 o
| :   1  3   :            :   2  6   : |
| ....6..5....            ....X..3.... |
|             ....Z..2....             |
|             :   5  6   :             |
T     3x1     8   7  4   3    3x3      o
o             7   8  3   4             V
|             :   2  1   :             |
|             ....6..5....             |
------o--o--------o--o--------o--o------
Player T's turn>
Player T's cards>
....1..2....  ....1..2....  ....1..2....  
:   6  8   :  :   8  3   :  :   7  5   :  
8   2  7   3  8   1  2   3  8   4  6   3  
7   3  5   4  7   4  7   4  7   1  8   4  
:   1  4   :  :   5  6   :  :   3  2   :  
....6..5....  ....6..5....  ....6..5....  
Select a card>
2
....1..2....
:   8  3   :
8   1  2   3
7   4  7   4
:   5  6   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
N
Enter a position>
3x1
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
| ....T..2....            ....7..8.... |
| :   6  8   :            :   1  5   : |
o 8   2  5   3    2x2     6   3  7   1 o
o 7   4  7   R            5   8  4   2 o
| :   1  3   :            :   2  6   : |
| ....6..5....            ....X..3.... |
| ....1..2........Z..2....             |
| :   8  3   ::   5  6   :             |
o 8   1  2   38   7  4   3    3x3      o
o 7   4  7   47   8  3   4             V
| :   5  6   ::   2  1   :             |
| ....6..5........6..5....             |
------o--o--------o--o--------o--o------
Player V's turn>
Player V's cards>
....1..2....  ....1..2....  ....1..2....  
:   7  6   :  :   8  6   :  :   6  4   :  
8   5  4   3  8   1  5   3  8   5  7   3  
7   1  3   4  7   4  7   4  7   3  2   4  
:   2  8   :  :   2  3   :  :   1  8   :  
....6..5....  ....6..5....  ....6..5....  
Select a card>
1
....1..2....
:   7  6   :
8   5  4   3
7   1  3   4
:   2  8   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
N  
Enter a position>
3x3
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
| ....T..2....            ....7..8.... |
| :   6  8   :            :   1  5   : |
o 8   2  5   3    2x2     6   3  7   1 o
o 7   4  7   R            5   8  4   2 o
| :   1  3   :            :   2  6   : |
| ....6..5....            ....X..3.... |
| ....1..2........Z..2........1..2.... |
| :   8  3   ::   5  6   ::   7  6   : |
o 8   1  2   38   7  4   38   5  4   V o
o 7   4  7   47   8  3   47   1  3   4 o
| :   5  6   ::   2  1   ::   2  8   : |
| ....6..5........6..5........6..5.... |
------o--o--------o--o--------o--o------
Player V lost!
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
| ....T..2....            ....7..8.... |
| :   6  8   :            :   1  5   : |
o 8   2  5   3    2x2     6   3  7   1 o
o 7   4  7   R            5   8  4   2 o
| :   1  3   :            :   2  6   : |
| ....6..5....            ....4..3.... |
| ....1..2........Z..2........1..2.... |
| :   8  3   ::   5  6   ::   7  6   : |
o 8   1  2   38   7  4   38   5  4   3 o
o 7   4  7   47   8  3   47   1  3   4 o
| :   5  6   ::   2  1   ::   2  8   : |
| ....6..5........6..5........6..X.... |
------o--o--------o--o--------o--o------
Player X lost!
------o--o--------o--o--------o--o------
|                         ....3..4.... |
|                         :   8  6   : |
o     1x1         1x2     Y   5  2   5 o
o                         1   7  4   6 o
|                         :   3  1   : |
|                         ....8..7.... |
| ....T..2....            ....7..8.... |
| :   6  8   :            :   1  5   : |
o 8   2  5   3    2x2     6   3  7   1 o
o 7   4  7   R            5   8  4   2 o
| :   1  3   :            :   2  6   : |
| ....6..5....            ....4..3.... |
| ....1..2........Z..2........1..2.... |
| :   8  3   ::   5  6   ::   7  6   : |
o 8   1  2   38   7  4   38   5  4   3 o
o 7   4  7   47   8  3   47   1  3   4 o
| :   5  6   ::   2  1   ::   2  8   : |
| ....6..5........6..5........6..5.... |
------o--o--------o--o--------o--o------
Player Y's turn>
Player Y's cards>
....1..2....  ....1..2....  
:   5  7   :  :   5  8   :  
8   4  6   3  8   2  7   3  
7   2  8   4  7   3  6   4  
:   3  1   :  :   4  1   :  
....6..5....  ....6..5....  
Select a card>
2  
....1..2....
:   5  8   :
8   2  7   3
7   3  6   4
:   4  1   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
1x2
Enter a char for rotate(R,L) or next(N)>
N
Enter a position>
2x1
Invalid position!
Player Y's turn.
Enter a position>
1x2
------o--o--------o--o--------o--o------
|             ....1..2........3..4.... |
|             :   5  8   ::   8  6   : |
o     1x1     8   2  7   32   5  2   5 o
o             Y   3  6   41   7  4   6 o
|             :   4  1   ::   3  1   : |
|             ....6..5........8..7.... |
| ....T..2....            ....7..8.... |
| :   6  8   :            :   1  5   : |
o 8   2  5   3    2x2     6   3  7   1 o
o 7   4  7   R            5   8  4   2 o
| :   1  3   :            :   2  6   : |
| ....6..5....            ....4..3.... |
| ....1..2........Z..2........1..2.... |
| :   8  3   ::   5  6   ::   7  6   : |
o 8   1  2   38   7  4   38   5  4   3 o
o 7   4  7   47   8  3   47   1  3   4 o
| :   5  6   ::   2  1   ::   2  8   : |
| ....6..5........6..5........6..5.... |
------o--o--------o--o--------o--o------
Player Z's turn>
Player Z's cards>
....1..2....  ....1..2....  
:   4  8   :  :   7  8   :  
8   2  5   3  8   2  4   3  
7   6  1   4  7   1  3   4  
:   7  3   :  :   5  6   :  
....6..5....  ....6..5....  
Select a card>
1
....1..2....
:   4  8   :
8   2  5   3
7   6  1   4
:   7  3   :
....6..5....
Enter a char for rotate(R,L) or next(N)>
N  
Enter a position>
2x2
Collide players !
------o--o--------o--o--------o--o------
|             ....1..2........3..4.... |
|             :   5  8   ::   8  6   : |
o     1x1     8   2  7   32   5  2   5 o
o             Y   3  6   41   7  4   6 o
|             :   4  1   ::   3  1   : |
|             ....6..5........8..7.... |
| ....T..2........1..2........7..8.... |
| :   6  8   ::   4  8   ::   1  5   : |
o 8   2  5   38   2  5   36   3  7   1 o
o Z   4  7   R7   6  1   45   8  4   2 o
| :   1  3   ::   7  3   ::   2  6   : |
| ....6..5........6..5........4..3.... |
| ....1..2........1..2........1..2.... |
| :   8  3   ::   5  6   ::   7  6   : |
o 8   1  2   38   7  4   38   5  4   3 o
o 7   4  7   47   8  3   47   1  3   4 o
| :   5  6   ::   2  1   ::   2  8   : |
| ....6..5........6..5........6..5.... |
------o--o--------o--o--------o--o------
Player Z lost!
------o--o--------o--o--------o--o------
|             ....1..2........3..4.... |
|             :   5  8   ::   8  6   : |
o     1x1     8   2  7   32   5  2   5 o
o             Y   3  6   41   7  4   6 o
|             :   4  1   ::   3  1   : |
|             ....6..5........8..7.... |
| ....T..2........1..2........7..8.... |
| :   6  8   ::   4  8   ::   1  5   : |
o 8   2  5   38   2  5   36   3  7   1 o
o 7   4  7   47   6  1   45   8  4   2 o
| :   1  3   ::   7  3   ::   2  6   : |
| ....6..5........6..5........4..3.... |
| ....1..2........1..2........1..2.... |
| :   8  3   ::   5  6   ::   7  6   : |
o 8   1  2   38   7  4   38   5  4   3 o
o 7   4  7   47   8  3   47   1  3   4 o
| :   5  6   ::   2  1   ::   2  8   : |
| ....6..5........6..R........6..5.... |
------o--o--------o--o--------o--o------
Player R lost!
------o--o--------o--o--------o--o------
|             ....1..2........3..4.... |
|             :   5  8   ::   8  6   : |
o     1x1     8   2  7   32   5  2   5 o
o             Y   3  6   41   7  4   6 o
|             :   4  1   ::   3  1   : |
|             ....6..5........8..7.... |
| ....T..2........1..2........7..8.... |
| :   6  8   ::   4  8   ::   1  5   : |
o 8   2  5   38   2  5   36   3  7   1 o
o 7   4  7   47   6  1   45   8  4   2 o
| :   1  3   ::   7  3   ::   2  6   : |
| ....6..5........6..5........4..3.... |
| ....1..2........1..2........1..2.... |
| :   8  3   ::   5  6   ::   7  6   : |
o 8   1  2   38   7  4   38   5  4   3 o
o 7   4  7   47   8  3   47   1  3   4 o
| :   5  6   ::   2  1   ::   2  8   : |
| ....6..5........6..5........6..5.... |
------o--o--------o--o--------o--o------
Winner player is Y !

 
 ```



