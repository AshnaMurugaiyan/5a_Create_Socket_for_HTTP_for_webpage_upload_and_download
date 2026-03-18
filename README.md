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
server.py
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

client.py
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
        f = open("cn.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("ashna.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
index.html
```
<!DOCTYPE html>
<html>
<head>
<title>My Page</title>
<style>
body{font-family:Arial;text-align:center;background:#f2f2f2}
h1{color:rgb(130, 9, 66)}
button{padding:10px;background:green;color:white;border:none}
</style>
</head>

<body>
<h1>Welcome</h1>
<p>Good Day</p>

<button onclick="alert('Hello! Have a Nice Day')">Click Me</button>

</body>
</html>
```

## OUTPUT
<img width="1652" height="972" alt="Screenshot 2026-03-18 133055" src="https://github.com/user-attachments/assets/7c5818e2-46fe-4ea7-bd96-886bb0fc692c" />
<img width="813" height="610" alt="Screenshot 2026-03-18 132443" src="https://github.com/user-attachments/assets/159935e1-45af-4ccb-ab64-2e3cb4960f25" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
