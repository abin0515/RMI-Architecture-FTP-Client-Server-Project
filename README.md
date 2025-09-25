# RMI Architecture - FTP Client-Server Project

A distributed File Transfer Protocol (FTP) client-server system implemented using Java RMI for distributed systems course assignment.

## 🏗️ Project Structure

```
Assignment1-Code/
├── ftp-interface/     # RMI interfaces and contracts
├── ftp-client/        # FTP client implementation
├── ftp-server/        # FTP server implementation
└── README.md
```

## 🚀 Quick Start

### Prerequisites
- Java 21+
- Maven 3.6+

### Build Project
```bash
cd Assignment1-Code/ftp
mvn clean package
```

## 🖥️ Local Testing

### Terminal 1: Start Server
```bash
cd ftp-server
java -jar target/ftp-server-1.0.0-jar-with-dependencies.jar
```

### Terminal 2: Start Client
```bash
cd ftp-client
java -jar target/ftp-client-1.0.0-jar-with-dependencies.jar
```

## ☁️ EC2 Testing

### Server Instance (EC2)
```bash
# Build on EC2
cd Assignment1-Code/ftp
mvn clean package

# Start server (replace with your EC2 public IP)
cd ftp-server
java -jar target/ftp-server-1.0.0-jar-with-dependencies.jar --serverIp YOUR_EC2_PUBLIC_IP
```

### Client Instance (Local or EC2)
```bash
# Start client pointing to EC2 server
cd ftp-client
java -jar target/ftp-client-1.0.0-jar-with-dependencies.jar --serverAddr YOUR_EC2_PUBLIC_IP
```

## 🧪 Testing Sequences

### Test Passive Mode
```bash
ftp> pasv                    # Set passive mode
PASV: Server in passive mode.
ftp> dir                     # List server files
ftp> get test.txt            # Download file
ftp> put upload_test.txt     # Upload file
ftp> dir                     # Verify upload
```

### Test Active Mode
```bash
ftp> port                    # Set active mode
PORT: Server in active mode.
ftp> dir                     # List server files
ftp> get readme.txt          # Download file
ftp> put upload_test.txt     # Upload file
ftp> dir                     # Verify upload
```

### Complete Test Cycle
```bash
# Create test file
echo "Test content" > test_file.txt

# Test all modes
ftp> pasv
ftp> put test_file.txt
ftp> port
ftp> get test_file.txt
ftp> ldir                    # List local files
```

## 📋 Available Commands

| Command | Description |
|---------|-------------|
| `get <file>` | Download file from server |
| `put <file>` | Upload file to server |
| `dir` | List server directory |
| `ldir` | List local directory |
| `pwd` | Show server working directory |
| `cd <dir>` | Change server directory |
| `pasv` | Set passive mode |
| `port` | Set active mode |
| `quit` | Exit client |

## 🔧 Configuration

### Server Properties (`ftp-server/src/main/resources/server.properties`)
```
server.path=root
server.name=ftpd
server.ip=localhost
server.port=5050
```

### Client Properties (`ftp-client/src/main/resources/client.properties`)
```
server.name=ftpd
server.ip=localhost
server.port=5050
client.ip=localhost
```

## 🏛️ Architecture

### RMI Control Layer
- **Registry**: Central lookup service (port 5050)
- **ServerFactory**: Creates server instances
- **Remote Methods**: `get()`, `put()`, `dir()`, `pwd()`, `cd()`

### Socket Data Layer
- **Passive Mode**: Server listens, client connects
- **Active Mode**: Client listens, server connects
- **Threading**: Concurrent file transfers

## 🎯 Features Implemented

- ✅ RMI connection setup
- ✅ Passive mode file download (GET)
- ✅ Passive mode file upload (PUT)
- ✅ Active mode file download (GET)
- ✅ Active mode file upload (PUT)
- ✅ Multi-threaded transfers
- ✅ Directory navigation
- ✅ Error handling

## 🐛 Troubleshooting

### Common Issues
1. **Connection Refused**: Check if server is running
2. **Empty Files**: Ensure flush/close operations
3. **Active Mode Fails**: Check firewall/NAT settings
4. **Port Already in Use**: Kill existing Java processes

### Debug Commands
```bash
# Check server logs
tail -f server.log

# Check network connections
netstat -an | grep 5050

# Test connectivity
telnet localhost 5050
```

## 📚 Learning Outcomes

This project demonstrates:
- **Distributed Systems**: RMI architecture patterns
- **Network Programming**: Socket communication
- **Concurrency**: Multi-threaded file transfers
- **Protocol Design**: FTP active/passive modes
- **System Integration**: Client-server coordination


