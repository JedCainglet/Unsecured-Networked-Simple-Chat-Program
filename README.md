# Unsecured-Networked-Simple-Chat-Program
Python chat program that uses network sockets to send messages via console user interface

## Adaptation and Base Issues to Address
This program was adapted from sentdex's YouTube tutorials on network sockets. This project's base code was taken from the following sources from sentdex: 
   - https://pythonprogramming.net/server-chatroom-sockets-tutorial-python-3/ 
   - https://pythonprogramming.net/client-chatroom-sockets-tutorial-python-3/
   
While the foundations of this code comes from these sources, the base code was found to have various issues, including: 
  - The client code cannot receive messages while waiting for user input (to send messages)
  - The client code does not have a user-friendly exit sequence for the user to leave the chat

## Approach / Solution
In particular, my aim for this project was to fix these two issues. The issue of receiving messages while being able to send messages could be resolved by implementing multithreading. One thread could be set to listen for any incoming messages, while the other thread could be used to wait for user input. 

The user-friendly exit sequence was simply a matter of implementing a user-input case that would allow the user to safely exit the program without "breaking" from the program. Pressing the enter / return key three times, or sending three empty messages in succession, is a simple way to allow the user to safely exit the program. While sending a certain message such as "/exit" or something similar would achieve the same effect, I felt that my idea would suffice in this case. 

An issue that arises from implementing both these solutions is the error message that produces from the thread listening for receiving messages. By executing the exit sequence, only one thread closes – the thread waiting on user input – while the other thread remains. Although simply terminating the listening thread right before the close of the user input thread would suffice, this project gave me the opportunity to learn and apply the concept of daemon threads. A daemon thread is initiated the same way as normal threads, but the difference is in the closing of the thread. Daemon threads automatically close on program exit. By making the listening thread a daemon thread, the thread closes once the main program exits. Once the user input thread executes the exit sequence, the main program can close safely without errors, taking the daemon thread down with it.

## Applications
This project can serve as a base component for computer science course assignments involving networking or security. The project implements sockets, so the project allows for a study on how network sockets are applied in Python. Since the project sends messages over plaintext (which is what makes it "unsecure"), this project can be improved upon to implement various security schemes to add security functionality. 
