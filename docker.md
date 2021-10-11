# Install Docker

- เพิ่มสิทธิ์ให้ Non-Root User สามารถรัน Docker ได้

  1. Create the docker group.

     ```shell
     sudo groupadd docker
     ```

  2. Add your user to the docker group.

     ```shell
     sudo usermod -aG docker $USER
     ```

  3. Log out and log back in so that your group membership is re-evaluated.

     If testing on a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.

     On a desktop Linux environment such as X Windows, log out of your session completely and then log back in.

     On Linux, you can also run the following command to activate the changes to groups:

     ```shell
     newgrp docker
     ```

  4. Verify that you can run docker commands without sudo.

     ```shell
     docker run hello-world
     ```

     This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

     If you initially ran Docker CLI commands using sudo before adding your user to the docker group, you may see the following error, which indicates that your ~/.docker/ directory was created with incorrect permissions due to the sudo commands.

     ```comment
     WARNING: Error loading config file: /home/user/.docker/config.json -stat /home/user/.docker/config.json: permission denied
     ```

     To fix this problem, either remove the ~/.docker/ directory (it is recreated automatically, but any custom settings are lost), or change its ownership and permissions using the following commands:

     ```shell
     sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
     sudo chmod g+rwx "$HOME/.docker" -R
     ```

  Reference [Post-installation steps for Linux - Manage Docker as a non-root user](https://docs.docker.com/engine/install/linux-postinstall/)
