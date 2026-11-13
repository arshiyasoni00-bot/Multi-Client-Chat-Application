# Multi-Client Chat Application (Java)

A runnable college project that combines Java OOP, multithreading, a Swing GUI, and TCP networking. One server can serve multiple chat clients at the same time.

## 🚀 Requirements

* **JDK 11 or later** (JDK 17 recommended)
* **No third-party libraries** required

## 💻 Run on Windows

1. **Download the Project**
   * Download the latest project package: **[multiclient-chat.zip](multiclient-chat.zip)**
   * Extract the project folder to your preferred local directory.
   *(Note: If you are using GitHub Releases, replace `multiclient-chat.zip` inside the parenthesis with your direct download URL).*

2. **Open the Terminal**
   * Open Command Prompt or the VS Code terminal inside the extracted folder.

3. **Verify Java installation**:
   ```bat
   java -version
   javac -version
   ```

4. **Start the Server** by double-clicking `run-server.bat`, or run:
   ```bat
   build.bat
   java -cp out chatapp.server.ChatServer 5000
   ```

5. **Start a Client** by double-clicking `run-client.bat`, or opening a second terminal and running:
   ```bat
   java -cp out chatapp.client.ChatClient
   ```

6. **Connect the Client**: Keep the host as `127.0.0.1`, port as `5000`, enter a username, and click **Connect**.

7. **Add more clients** by running `run-client.bat` again. Type `/quit` or click **Disconnect** to leave.

*Note: The server automatically writes chat events to `chat-history.log` in its current working directory.*

## 🌐 Connect from another computer (Same Wi-Fi/LAN)

1. **Start the server** on the host computer.
2. **Find the host IP**: Open a terminal on the host computer and run `ipconfig` to find its local IPv4 address.
3. **Connect clients**: Run the client on other computers and enter the host computer's IPv4 address instead of `127.0.0.1` (keep port `5000`).
4. **Firewall**: Allow Java through the Windows Firewall on a trusted private network if prompted.

⚠️ *Do not expose this server to the public internet without adding authentication, encryption (TLS), and appropriate security controls.*

## 📁 Project Structure

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

## ⚙️ How It Works

* **ChatServer**: Opens a `ServerSocket` and continuously accepts incoming client sockets.
* **ClientHandler**: Implements `Runnable`; each unique connection is handled by a separate background thread.
* **Broadcasting**: Each client sends its username first, followed by message payloads. The server broadcasts these payloads to all connected clients.
* **ChatClient**: Extends `JFrame` to provide the Swing graphical user interface. A separate reader thread handles incoming data to keep the UI responsive.
* **ChatMessage**: Models a text message as an immutable object.
* **ChatLogger**: Linearly appends runtime server events to a plain text log file.

## 🔒 Security & Educational Disclaimer

This is an educational LAN demo application. It does not encrypt network traffic or verify user identities. Do not use it for confidential communication as-is. Username validation and message-length limits act as basic safeguards, not a production-grade security system.
