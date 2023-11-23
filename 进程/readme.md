## 僵尸进程如何形成

僵尸进程（Zombie Process）是指一个已经终止执行的进程，但是其在进程表中的表项仍然保留，并且系统仍然为其保留一些资源，如进程标识符（PID）等。僵尸进程的形成通常发生在以下情况：

进程终止： 当一个进程调用 exit 系统调用或者返回了 main 函数时，它会变成僵尸进程。这时，进程的用户空间代码已经执行完毕，但内核仍然保留了进程的一些信息。

父进程未处理子进程退出状态： 当一个子进程终止时，内核会向其父进程发送一个 SIGCHLD 信号，通知父进程子进程已经终止。父进程需要通过调用 wait 或 waitpid 系统调用来获取子进程的退出状态。如果父进程没有正确处理这个信号，子进程就会变成僵尸进程。

下面是一个简单的示例，演示了僵尸进程的形成：

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    pid_t child_pid = fork();

    if (child_pid == -1) {
        // 错误处理
        perror("fork");
        exit(EXIT_FAILURE);
    }

    if (child_pid == 0) {
        // 子进程
        printf("Child process is exiting.\n");
        exit(EXIT_SUCCESS);
    } else {
        // 父进程
        sleep(2);  // 等待子进程退出
        printf("Parent process is exiting.\n");
    }

    return 0;
}

在上述示例中，父进程在 sleep(2) 之前退出，而没有等待子进程的退出状态。这会导致子进程成为僵尸进程，因为父进程没有处理 SIGCHLD 信号。

要避免僵尸进程，父进程应该通过 wait 或 waitpid 来等待子进程的退出状态，从而允许内核释放子进程的资源。例如，在父进程中可以使用以下代码：

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    pid_t child_pid = fork();

    if (child_pid == -1) {
        // 错误处理
        perror("fork");
        exit(EXIT_FAILURE);
    }

    if (child_pid == 0) {
        // 子进程
        printf("Child process is exiting.\n");
        exit(EXIT_SUCCESS);
    } else {
        // 父进程
        wait(NULL);  // 等待子进程退出状态
        printf("Parent process is exiting.\n");
    }

    return 0;
}

在这个例子中，父进程使用 wait(NULL) 等待子进程的退出状态，确保子进程不会变成僵尸进程。
