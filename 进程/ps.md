# ps

### 有没有ps查不到的进程
```
是的，有一些进程可能无法通过常规的 ps 命令或类似工具来查看，这取决于进程的权限级别、进程的状态以及操作系统的类型和配置等因素。以下是一些可能无法通过 ps 命令查看的进程：

内核线程（Kernel threads）：这些进程运行在内核空间中，通常不会被列在用户空间进程列表中。如果您想查看所有进程，可以尝试使用 ps -eLf 命令。

被隐藏的进程（Hidden processes）：一些恶意软件可能会隐藏其进程，以避免被发现。这些进程通常使用 root 权限，可以通过 ps 命令的 -x 选项来查看。

线程（Threads）：在某些情况下，多个线程可能会共享相同的进程 ID，因此它们不会被列为独立的进程。您可以尝试使用 ps -eLf 命令来查看所有线程。

僵尸进程（Zombie processes）：这些进程已经完成了它们的工作，但是它们的进程描述符仍然存在于系统中，以便它们的父进程可以读取它们的退出状态。这些进程通常不会出现在 ps 命令的输出中，但可以通过 ps axo stat,ppid,pid,comm | grep -w Z 命令查看。

容器进程（Container processes）：在容器化的环境中，一些进程可能是在容器中运行的，这些进程可能无法通过 ps 命令查看。您可以尝试使用 Docker 或其他容器管理工具来查看容器中运行的进程。

总之，如果您发现无法通过 ps 命令查看某些进程，可能是因为这些进程处于特殊的状态或权限级别下，您可以尝试使用其他工具来获取更多信息。
```


### ps -x命令返回的字段分别是什么意思
```
ps -x 命令是在 Linux 系统上查看所有进程的命令。它返回的字段如下：

css
Copy code
  PID TTY      STAT   TIME COMMAND
PID：进程 ID，即进程的唯一标识符。

TTY：该进程关联的终端设备或伪终端设备。如果进程没有关联的终端设备，则为 ?。

STAT：进程状态，其中常见的状态包括：

R：运行中（running）
S：休眠中（sleeping）
D：不可中断的休眠状态（uninterruptible sleep）
Z：僵尸状态（zombie）
T：停止或跟踪状态（stopped or traced）
<：高优先级（high-priority）
N：低优先级（low-priority）
TIME：该进程消耗的 CPU 时间，包括用户态（user time）和内核态（system time）。

COMMAND：该进程的命令行名称和参数。

注意，ps -x 命令显示的是所有进程，包括系统进程和用户进程，因此可能会显示大量的进程信息。如果您只想查看当前终端会话中的进程，请使用 ps -x | grep $$ 命令，其中 $$ 表示当前 Shell 进程的进程 ID。
```


### 为什么容器进程无法通过ps查看
```
容器技术通常会使用隔离的命名空间和进程空间来运行容器中的应用程序。这意味着容器中的进程和宿主机上的进程被隔离开来，因此在宿主机上运行的 ps 命令无法查看容器中的进程。

具体地说，容器中的进程运行在自己的命名空间中，这包括 PID 命名空间。在容器内运行的进程的 PID 是在容器内部使用的，因此在宿主机上的 ps 命令无法查看这些 PID。

通常情况下，您可以使用容器管理工具来查看容器中的进程，例如 docker ps 或 kubectl get pods 等命令。这些工具可以与 Docker 引擎或 Kubernetes 集群交互，并显示容器的状态、进程和其他相关信息。

此外，您也可以使用 docker exec 命令进入到容器中，并在容器内部运行 ps 命令来查看容器中的进程。例如：

docker exec <container_name_or_id> ps aux

这将在容器中运行 ps 命令，并显示容器中的所有进程。

```


### 如果系统内有多个docker容器进程，那么通过ps命令会看到什么

```
在宿主机上使用 ps 命令可以查看系统上所有进程的信息，包括所有正在运行的 Docker 容器进程。但是，由于容器技术使用命名空间和进程空间来隔离容器中的进程和宿主机上的进程，因此在 ps 命令的输出中，您将看到每个正在运行的 Docker 容器进程的 PID、COMMAND 和其他信息。

在 ps 命令的输出中，每个 Docker 容器进程都会以其命令行的形式显示。通常情况下，这些命令行都包含有关容器映像的信息，例如容器的名称、映像 ID、容器 ID 等。例如：

1234 ?        Sl     0:00 /usr/bin/dockerd --foreground --config-file=/etc/docker/daemon.json
5678 ?        Ssl    0:00 containerd --config /var/run/docker/containerd/containerd.toml --log-level info
9012 ?        Sl     0:00 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 8080 -container-ip 172.17.0.2 -container-port 80

在这个示例中，您可以看到三个不同的 Docker 容器进程，其中一个是 Docker 守护进程，一个是 containerd 进程，另一个是 Docker 代理进程。这些进程的 PID 和其他信息也可以在 ps 命令的输出中看到。

总之，使用 ps 命令可以在宿主机上查看所有进程的信息，包括正在运行的 Docker 容器进程的信息。如果您只想查看 Docker 容器进程的信息，请使用 docker ps 命令。
```
