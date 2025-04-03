# Multi-Client-Chat-Server

Features 
Implemented Features: 
● TCP-based server that listens on port 8080 
● Handles multiple concurrent client connections 
● User authentication using users.txt 
● Supports private messaging (/msg <username> <message>) 
● Supports broadcasting messages (/broadcast <message>) 
● Group messaging (/group_msg <group_name> <message>) 
● Group management: 
/create_group <group_name> to create a group 
/join_group <group_name> to join a group 
/leave_group <group_name> to leave a group 
Not Implemented Features: 
● GUI-based client interface (currently text-based only) 
● Persistent storage for messages across sessions 
Design Decisions 
Multi-threading Approach 
● A new thread is created for each client connection to handle multiple clients 
concurrently. 
● std::mutex is used to synchronize access to shared data structures such as user 
lists and group mappings. 
● The server maintains three main data structures: 
1. std::unordered_map<int, std::string>: Maps client socket 
descriptors to usernames. 
2. std::unordered_map<std::string, std::string>: Maps 
usernames to passwords. 
3. std::unordered_map<std::string, std::unordered_set<int>>: 
Maps group names to client socket descriptors. 
Synchronization Decisions 
● Used std::lock_guard<std::mutex> for thread-safe access to shared 
resources. 
● Prevented race conditions by locking before modifying shared data structures. 
Implementation 
High-Level Overview 
● Server Initialization 
1. Creates a socket and binds it to a port. 
2. Listens for incoming client connections. 
●       Client Connection Handling 
1. Authenticates user using users.txt. 
2. Spawns a new thread to handle client communication. 
● Command Processing 
1. Parses incoming messages to determine the type of command (/msg, 
/broadcast, etc.). 
2. Executes the appropriate action. 
● Group Management 
1. Handles group creation, joining, and leaving. 
Code Flow 
1. Server starts and listens for connections. 
2. Client connects and enters username/password. 
3. Server authenticates the client. 
4. Client sends messages (private, broadcast, or group messages). 
5. Server routes messages appropriately. 
6. Client disconnects, and server removes them from active clients and groups. 
Testing 
Correctness Testing 
● Verified authentication by providing valid and invalid credentials. 
● Checked message delivery for private messages, broadcasts, and group messages. 
Stress Testing 
● Simulated multiple concurrent client connections. 
● Tested message handling under high traffic. 
Challenges & Solutions 
● Handling concurrent client connections → Used multi-threading with 
std::mutex. 
● Ensuring thread safety → Used std::lock_guard<std::mutex> for shared 
resources. 
● Parsing user commands correctly → Used std::string::find() and 
substr(). 
● Debugging segmentation faults → Added proper error handling and logging. 
Restrictions 
● Maximum clients: Limited by system resources and thread handling. 
● Maximum groups: Theoretically unlimited but constrained by memory. 
● Maximum message size: 1024 bytes per message. 
Individual Contributions 
● Tanmey Agarwal(211098) : Server architecture, threading, synchronization 
● Kumar Kanishk Singh(210544) : Message handling, group management, 
authentication 
● Sunny Raja Prasad(218171078): Testing, debugging, documentation (README) 
Sources 
● Beej’s Guide to Network Programming 
● C++ Reference for std::mutex, std::unordered_map 
● GeeksforGeeks articles on multi-threading and socket programming 
Declaration 
● We declare that this assignment was completed independently without plagiarism. 
Feedback 
● The assignment was well-structured and helped in understanding multi-threaded 
socket programming. 
● Some clarifications regarding the expected behavior of group messaging would have 
been helpful.
