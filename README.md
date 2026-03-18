# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
server.py
```
import socket
print("SERVER FILE STARTED")

port = 60000
s = socket.socket()
host = socket.gethostname()

s.bind((host, port))
s.listen(5)

print("Server is running...")
print("Waiting for client connection...")

while True:
    conn, addr = s.accept()
    print("Connected to:", addr)

    data = conn.recv(1024)
    print("Server received:", data.decode())

    with open("mytext.txt", "rb") as f:
        while True:
            chunk = f.read(1024)
            if not chunk:
                break
            conn.send(chunk)

    print("Done sending file")
    conn.send(b"\nThank you for connecting")
    conn.close()
```
client.py
```
import socket

s = socket.socket()
host = socket.gethostname()
port = 60000

s.connect((host, port))
s.send("Hello server!".encode())

with open('mytext.txt', 'wb') as f:
    while True:
        print('Receiving data...')
        data = s.recv(1024)
        if not data:
            break
        f.write(data)

print('Successfully received the file')

# Open and Read File
print("\nFile Content:")
with open("mytext.txt", "r") as f:
    print(f.read())

s.close()
print('Connection closed')
```
## OUPUT
<img width="1033" height="202" alt="image" src="https://github.com/user-attachments/assets/f2391fea-3e0e-4b6a-9ebd-ec763277a851" />


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
