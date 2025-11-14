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
## client:
```
import socket

s = socket.socket()
host = socket.gethostname()
port = 60000
s.connect((host, port))
s.send(b"Hello server!")  # Fixed: encode as bytes

with open("received_file.txt", "wb") as f:  # Fixed: added file extension
    while True:
        print("receiving data...")
        data = s.recv(1024)
        print(f"data={data}")  # Fixed: proper string formatting
        if not data:
            break
        f.write(data)

print("successfully get the file")
s.close()
print("connection closed")
```
## server
```
import socket

port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)  # Fixed: added backlog parameter

while True:
    conn, addr = s.accept()
    data = conn.recv(1024)
    print("Server received", repr(data))
    
    filename = "mytext.txt"
    try:
        f = open(filename, "rb")
        l = f.read(1024)
        while l:
            conn.send(l)
            print("Sent ", repr(l))
            l = f.read(1024)
        f.close()
        print("Done sending")
        conn.send(b"Thank you for connecting")  # Fixed: encode as bytes
    except FileNotFoundError:
        print(f"File {filename} not found")
        conn.send(b"Error: File not found")
    
    conn.close()
```
## OUPUT
<img width="1067" height="297" alt="image" src="https://github.com/user-attachments/assets/57a00658-d492-492f-9dda-30b7a12ffe2b" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
