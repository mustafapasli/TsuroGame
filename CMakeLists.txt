cmake_minimum_required(VERSION 3.9)
project(TsuroGame)

set(CMAKE_CXX_STANDARD 11)

add_executable(TsuroGame
        Card.cpp
        Card.h
        Grid.cpp
        Grid.h
        main.cpp
        Player.cpp
        Player.h
        Tsuro.cpp
        Tsuro.h)
