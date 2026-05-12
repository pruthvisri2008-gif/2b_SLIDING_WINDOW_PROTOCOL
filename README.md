# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To implement a program to illustrate the mechanism of sliding window protocol.
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
~~~
server.py
import socket
s = socket.socket()
s.bind(('localhost', 8002))
s.listen(5)
print("Server is waiting for connection...")
c, addr = s.accept()
print("Connected to:", addr)
while True:
    data = c.recv(1024).decode()

    if not data:
        break

    print("Received Frames:", data)

    c.send("Acknowledgement received".encode())

c.close()
~~~
client.py

~~~
import socket

s = socket.socket()

s.connect(('localhost', 8002))

list_size = int(input("Enter the number of frames to send: "))

frames = list(range(list_size))

window_size = int(input("Enter Window Size: "))

start = 0

while start < list_size:

    window = frames[start:start + window_size]

    s.send(str(window).encode())

    print("Sent Frames:", window)

    ack = s.recv(1024).decode()

    print("Server:", ack)

    start += window_size

s.close()
~~~
## OUPUT
<img width="1409" height="353" alt="cn exp02b" src="https://github.com/user-attachments/assets/7b681965-32c8-4d54-b926-f26dc3cfb757" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
