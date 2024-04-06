# explain in details what exactly docker virtualizes while running on ubuntu

Docker is a containerization platform that allows you to package applications and their dependencies into isolated and portable containers. When running on Ubuntu, Docker virtualizes the operating system kernel and its resources, enabling you to run multiple containers on the same host machine while maintaining isolation between them.

Here's a more detailed explanation of what Docker virtualizes when running on Ubuntu:

1. **Operating System Kernel**: Docker leverages the Linux kernel's virtualization features, such as namespaces and cgroups, to provide an isolated environment for each container. Namespaces handle the isolation of various system resources, such as process trees, network interfaces, mount points, and inter-process communication (IPC) resources. This ensures that each container has its own isolated view of these resources, preventing conflicts and interference between containers.

2. **File System**: Docker uses union file systems, such as OverlayFS (the default on Ubuntu), to layer multiple file system layers (read-only base image and read-write container layer) into a single unified file system view for each container. This allows containers to share the same base image while maintaining their own writable layer for modifications.

3. **Network Stack**: Docker creates a virtual network interface for each container and manages the networking namespace, allowing containers to have their own network stack, including IP addresses, routing tables, and firewall rules. This enables containers to communicate with each other and the host machine seamlessly.

4. **Process Tree**: Docker utilizes process namespaces to isolate the process tree for each container. Each container has its own init process (PID 1) and its own set of child processes, independent from other containers and the host system's process tree.

5. **Resource Constraints**: Docker leverages control groups (cgroups) to limit and control the resources (CPU, memory, disk I/O, network bandwidth) that each container can consume. This prevents a single container from monopolizing the host's resources and ensures fair resource allocation among containers.

6. **User Namespaces (Optional)**: Docker can also utilize user namespaces to map the user and group IDs inside a container to different values on the host system. This enhances security by preventing potential conflicts between the container's and host's user/group IDs.

It's important to note that Docker containers do not virtualize the entire operating system kernel like traditional virtual machines (VMs). Instead, Docker containers share the host's kernel, making them more lightweight and efficient compared to VMs. This also means that containers running on Ubuntu are limited to the capabilities and architecture of the underlying Ubuntu host kernel.

Docker's virtualization approach allows for efficient resource utilization, portability, and isolation, making it a popular choice for deploying and managing applications on Ubuntu and other Linux distributions.
