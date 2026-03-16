# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>

## Program
server :
```
import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()

```
client :
```
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
index.html :
```
<!DOCTYPE html>
<html>
<head>
    <title>My First Web Page</title>
</head>

<body>

<h1>Welcome to My Website</h1>
<p>This is my first HTML program.</p>

</body>
</html>
```
## OUTPUT
<img width="1221" height="88" alt="image" src="https://github.com/user-attachments/assets/08fad982-4192-468c-bb73-2fcf537b3247" />
<img width="1271" height="596" alt="image" src="https://github.com/user-attachments/assets/191339ee-77c7-4ffc-9b6a-79b66fe92504" />
<img width="785" height="112" alt="image" src="https://github.com/user-attachments/assets/ab3a7be4-02bd-4081-a4cf-a8bb491f6cca" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
