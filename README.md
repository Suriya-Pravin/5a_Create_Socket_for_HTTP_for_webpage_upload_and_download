# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download

## AIM  
To write a PYTHON program for socket for HTTP for web page upload and download

## Algorithm

1. Start the program.  
2. Get the frame size from the user.  
3. Create the frame based on the user request.  
4. Send frames to server from the client side.  
5. If your frames reach the server, it will send ACK signal to client; otherwise, it will send NACK signal to client.  
6. Stop the program.

## Program  
**Name:** Suriya Pravin M  
**Reg No:** 212223230223  

```python
import socket

def send_request(host, port, request):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        s.sendall(request.encode())
        response = s.recv(4096).decode()
    return response

def upload_file(host, port, filename):
    with open(filename, 'rb') as file:
        file_data = file.read()
        content_length = len(file_data)
        request = f"POST /upload HTTP/1.1\r\nHost: {host}\r\nContent-Length: {content_length}\r\n\r\n{file_data.decode()}"
        response = send_request(host, port, request)
    return response

def download_file(host, port, filename):
    request = f"GET /{filename} HTTP/1.1\r\nHost: {host}\r\n\r\n"
    response = send_request(host, port, request)

    file_content = response.split('\r\n\r\n', 1)[1]
    with open(filename, 'wb') as file:
        file.write(file_content.encode())

if __name__ == "__main__":
    host = 'example.com'
    port = 80

    upload_response = upload_file(host, port, 'MyFile.txt')
    print("Upload response:", upload_response)

    download_file(host, port, 'MyFile.txt')
    print("File downloaded successfully.")
```

## OUTPUT  
![Screenshot 2025-05-18 143835](https://github.com/user-attachments/assets/623927c0-a0f1-4069-b701-1982613f6101)

## Result  
Thus the socket for HTTP for web page upload and download was created and executed.
