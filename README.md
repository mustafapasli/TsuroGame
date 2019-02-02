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
