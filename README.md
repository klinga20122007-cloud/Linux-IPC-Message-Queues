# Linux-IPC-Message-Queues
Linux IPC-Message Queues

# AIM:
To write a C program that receives a message from message queue and display them

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux message queues API 

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## C program that receives a message from message queue and display them
```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

// Structure for message
struct message
{
    long msg_type;
    char text[100];
};

int main()
{
    struct message msg;

    // Generate unique key
    key_t key = ftok("progfile", 65);

    // Create/Get message queue
    int msgid = msgget(key, 0666 | IPC_CREAT);

    // Receive message
    msgrcv(msgid, &msg, sizeof(msg.text), 1, 0);

    // Display message
    printf("Message Received: %s\n", msg.text);

    // Destroy message queue
    msgctl(msgid, IPC_RMID, NULL);

    return 0;
}                              RECEIVER
```
```

#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

// Structure for message
struct message
{
    long msg_type;
    char text[100];
};

int main()
{
    struct message msg;

    // Generate unique key
    key_t key = ftok("progfile", 65);

    // Create/Get message queue
    int msgid = msgget(key, 0666 | IPC_CREAT);

    msg.msg_type = 1;

    printf("Enter Message: ");
    fgets(msg.text, sizeof(msg.text), stdin);

    // Send message
    msgsnd(msgid, &msg, sizeof(msg.text), 0);

    printf("Message Sent: %s\n", msg.text);

    return 0;
}                     SENDER
```


## OUTPUT
<img width="748" height="633" alt="image" src="https://github.com/user-attachments/assets/6f17a880-24b4-4208-8ec4-815ad708033d" />




# RESULT:
The programs are executed successfully.
