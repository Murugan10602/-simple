# -simple
import socket
import threading

def handle_client(client_socket):
    while True:
        data = client_socket.recv(1024)
        print(f"Received: {data.decode()}")
        client_socket.send(data)

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('0.0.0.0', 8080))
server.listen(5)
print("Server listening on port 8080")

while True:
    client, addr = server.accept()
    print(f"Accepted connection from {addr[0]}:{addr[1]}")
    client_handler = threading.Thread(target=handle_client, args=(client,))
    client_handler.start()
