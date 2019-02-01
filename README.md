# TsuroGame
Tsuro Game Implementation in C++

Tsuro
• Read the explanations about the original game (https://en.wikipedia.org/wiki/Tsuro)

Basic Elements of the Game Tokens
• Tokens represent players.
• For the version you are going to implement, tokens will be displayed as single characters.

Path Cards
• Square cards which have 2 ports on each of their sides and various routing information. • You can display a Path card as follows:
....1..2.... 
:   8  6   : 
8   1  5   3 
7   4  7   4 
:   2  3   : 
....6..5....

• Here, ports are numbered (1,2,3,4,5,6,7,8).
• Inside, the routing information is presented. For the particular card above:
– port 8 is connected to port 1 – port 7 is connected to port 4 – port 6 is connected to port 2 – port 5 is connected to port 3
• Connections are not directed.
• A path card can be rotated clockwise or counter-clockwise(repeatedly)

2D grid
• This game will be played on a 2D grid.
• Each cell on this grid will either be occupied by a path card or it will be empty. • Cards can only be placed in empty cells
• Below is an example of a partially filled 3x3 grid

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

• On the sides of the grid 'o's represent exit/entry ports of the game.
• A User token may start at any of the exit/entry ports and exit from any of the ports.
• If the ports of path cards(tiles) collide, they are assumed to be connected. For example, port 3 of the tile 1
(first row, first column) is connected to port 6 of the tile on the right.

Rules of The Game
• For a general understanding of the game please read the necessary wikipedia articles. You can find more information on other webpages.
• Basically:
– It is a turn-based game.
– There are at least 2 players, each one has a token.
– Game starts randomly. (random entry ports are chosen for each player)
– Initially, the 2D grid is empty.
– Each player is given a set of cards(Generally 3 cards.)
– A turn starts with the player deciding on a card(selecting a card from the set given). If the set of cards
is empty, a new set is requested (how you generate a set is up to you. It has to be flexible for further
modifications. So hide unnecessary details.)
– Once a card is selected, it is placed in an empty cell on the 2D grid.
– The token follows the route on the card placed.
– The objective is to remain on the game.

Example:
• Initial. Player1(token X) places a path card:

------X--o--------o--o--------o--o------ 
| ....1..2....                         | 
| :   8  6   :                         | 
o 8   1  5   3                         o 
Y 7   4  7   4                         o 
| :   2  3   :                         | 
| ....6..5...                          | 
|                                      | 
|                                      | 
o                                      o 
o                                      o 
|                                      | 
|                                      | 
|                                      | 
|                                      | 
o                                      o 
o                                      o 
|                                      | 
|                                      | 
------o--o--------o--o--------o--o------

• With the tile which is recently placed, the game advances. X follows the path and exist the game(loses). Y follows its path and waits for the next event.
• It’s Player2(token Y)’s turn:
------o--o--------o--o--------o--o------ 
| ....1..2....                         | 
| :   8  6   :                         | 
X 8   1  5   3                         o 
o 7   4  7   Y                         o 
| :   2  3   :                         | 
| ....6..5...                          | 
| ....3..4....                         | 
| :   4  3   :                         |
o 2   1  6   5                         o 
o 1   2  5   6                         o 
| :   7  8   :                         | 
| ....8..7....                         | 
|                                      | 
|                                      | 
o                                      o 
o                                      o 
|                                      | 
|                                      | 
------o--o--------o--o--------o--o------
• At this stage there isn’t any other player, so Y wins.
