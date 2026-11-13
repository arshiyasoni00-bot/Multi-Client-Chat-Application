# Multi-Client Chat Application (Java)

A small, runnable college project that combines Java OOP, multithreading, a Swing GUI, and TCP networking. One server can serve multiple chat clients at the same time.

## Requirements

- JDK 11 or later (JDK 17 recommended)
- No third-party library is required

## Run on Windows

1. Extract the project folder.
2. Open Command Prompt or the VS Code terminal in this folder.
3. Check Java is installed:

   ```bat
   java -version
   javac -version
   ```

4. Start the server by double-clicking `run-server.bat`, or run:

   ```bat
   build.bat
   java -cp out chatapp.server.ChatServer 5000
   ```

5. Start a client by double-clicking `run-client.bat`, or in a second terminal run:

   ```bat
   java -cp out chatapp.client.ChatClient
   ```

6. In the client, keep host as `127.0.0.1`, port as `5000`, enter a username, and click **Connect**.
7. Run the client again to open additional clients. Each connected client receives messages from all users. Type `/quit` or click **Disconnect** to leave.

The server writes chat events to `chat-history.log` in its current working directory.

## Connect from another computer on the same Wi-Fi/LAN

1. Start the server on the host computer.
2. Find that computer's local IPv4 address using `ipconfig` on Windows.
3. On each other computer, start the client and enter the host computer's IPv4 address instead of `127.0.0.1`; keep port `5000`.
4. Allow Java through the Windows Firewall on a trusted private network if Windows asks. Do not expose the server to the public internet without adding authentication, encryption (TLS), and appropriate security controls.

## Project structure

```text
multiclient-chat/
├── src/
│   └── chatapp/
│       ├── client/
│       │   └── ChatClient.java
│       ├── common/
│       │   ├── ChatLogger.java
│       │   └── ChatMessage.java
│       └── server/
│           ├── ChatServer.java
│           └── ClientHandler.java
├── build.bat
├── run-client.bat
├── run-server.bat
└── README.md
```

## How it works

- `ChatServer` opens a `ServerSocket` and accepts many client sockets.
- `ClientHandler` implements `Runnable`; every connection is handled by a separate thread.
- Each client sends its username first, then sends one message per line. The server broadcasts each message to the connected clients.
- `ChatClient` extends `JFrame` to provide the graphical user interface. A separate reader thread keeps the GUI responsive.
- `ChatMessage` models a message as an immutable object.
- `ChatLogger` appends server events to a text file.

## Important notes

This is an educational LAN/demo application. It does not encrypt traffic or verify user identities. Do not use it for confidential communication as-is. Username checks and message-length limits are basic safeguards, not a complete security system.
