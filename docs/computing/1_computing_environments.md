# Setting up a streamlined computing environment

## Setting up your `ssh` config
This code snippet is used to configure an SSH connection.

The SSH configuration file allows you to define various settings for SSH connections, such as host aliases, port numbers, and identity files. This file is typically located at ~/.ssh/config.

To create a starter SSH config, follow these tips:

1. Open a terminal or command prompt.
2. Navigate to your home directory by running the command `cd ~`.
3. Create a new file named `config` in the `.ssh` directory by running the command `touch ~/.ssh/config`.
4. Open the `config` file in a text editor of your choice.
5. Add the desired SSH configuration settings using the following format:

```
Host <alias>
     HostName <hostname>
     Port <port>
     User <username>
     IdentityFile <path_to_private_key>
     LocalForward <connection_port> localhost:<connection_port>
     ControlMaster auto
     ControlPersis yes
```

Replace `<alias>` with a unique name for the host alias, `<hostname>` with the IP address or domain name of the remote server, `<port>` with the SSH port number (default is 22, usually you can omit this), `<username>` with your username on the remote server, and `<path_to_private_key>` with the path to your private key file. 

The `LocalForward` part is useful for when you need to connect to a web application running on the remote server, such as Tensorboard or the dask dashboard. Once your application is running you can connect to it on your local machine by pointing your web browser to `localhost:<connection_port>`. You may have to play around with the number used for `<connection_port>`, as different systems use different ports for system applications.

Setting `ControlMaster` and `ControlPersist` are just useful for when you want to have multiple connections to the same server, so we suggest generally setting them as specified above, though this is not strictly necessary.

6. Save the `config` file.

You can now use the defined host aliases in your SSH commands to connect to remote servers easily.

!!! note 

    Make sure to set appropriate permissions for the `config` file by running the command `chmod 600 ~/.ssh/config` to ensure it is only readable by you.


## Passwordless login with ssh keys

Setting up passwordless login with SSH keys allows you to securely authenticate with remote servers without having to enter a password each time. Here's how you can set it up:

1. Generate an SSH key pair on your local machine if you don't already have one. You can do this by running the command `ssh-keygen` in your terminal. This will generate a public key (`id_rsa.pub`) and a private key (`id_rsa`) in the `~/.ssh` directory.

2. Copy the public key to the remote server by running the command `ssh-copy-id <username>@<hostname>`. Replace `<username>` with your username on the remote server and `<hostname>` with the IP address or domain name of the remote server. This command will copy your public key to the `~/.ssh/authorized_keys` file on the remote server, allowing you to authenticate using your private key.

3. Test the passwordless login by running the command `ssh <username>@<hostname>`. You should be able to log in without entering a password.

With passwordless login set up, you can now easily and securely connect to remote servers using SSH keys.

!!! note

    Make sure to keep your private key (`id_rsa`) secure and never share it with anyone. If your private key is compromised, an attacker could gain unauthorized access to any remote servers you have set this up for. We suggest setting permissions to `600` in the same way as is recommended in the note on the ssh config section.


## Using `tmux` for persistent sessions

`tmux` is a powerful terminal multiplexer that allows you to create and manage multiple terminal sessions within a single window. It provides a way to keep your sessions running even if you disconnect from the server or close your terminal.

Here are some basic usage tips for `tmux`:

1. Start a new `tmux` session by running the command `tmux` in your terminal.

2. Once inside `tmux`, you can create new windows by pressing `Ctrl+b` followed by `c`. This will open a new window with a shell prompt.

3. To switch between windows, use `Ctrl+b` followed by a number key corresponding to the window you want to switch to. For example, `Ctrl+b 0` will switch to window 0, `Ctrl+b 1` will switch to window 1, and so on.

4. You can also navigate between windows using `Ctrl+b` followed by `n` (next window) or `p` (previous window).

5. To split a window into multiple panes, use `Ctrl+b` followed by `%` (vertical split) or `"` (horizontal split). This will divide the current window into two panes, allowing you to run different commands side by side.

6. To navigate between panes, use `Ctrl+b` followed by an arrow key in the direction you want to move. For example, `Ctrl+b` followed by `Left Arrow` will move to the pane on the left.

7. To resize panes, press `Ctrl+b` followed by `Ctrl+Arrow Key` in the direction you want to resize. For example, `Ctrl+b` followed by `Ctrl+Right Arrow` will increase the width of the current pane.

8. If you need to detach from a `tmux` session and leave it running in the background, press `Ctrl+b` followed by `d`. You can then safely close your terminal or disconnect from the server.

9. To reattach to a detached `tmux` session, use the command `tmux attach` in your terminal.

These are just some of the basic `tmux` commands to get you started. `tmux` has many more features and customization options, so be sure to check out the documentation for more advanced usage.

!!! tip

    The default `tmux` experience is not very user friendly - we suggest customizing your experience by creating a configuration file at `~/.tmux.conf`. [This tutorial](https://hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/) is a great starting point. Similarly, you can see Andrew's configuration [here](https://github.com/arbennett/dotfiles/blob/master/tmux.conf).


## Accessing remote `jupyter` servers
To access a remote Jupyter server using forwarded ports, you can follow these steps:

1. Start by configuring your SSH connection to forward ports. To see how to do this see the section on setting up your ssh config.
3. Connect to the remote server using SSH by running the command `ssh <alias>` in your terminal. This will establish the SSH connection and forward the specified ports.

4. Once connected to the remote server, start the Jupyter server by running the command `jupyter lab --no-browser --port=<remote_port>`. Replace `<remote_port>` with the same port number specified in the SSH config file.

5. The Jupyter server will start and display a URL in the terminal. Copy the URL and access it from your local machine's web browser.

You should now be able to access and use the remote Jupyter server from your local machine using forwarded ports.


## Installing `conda` on remote servers

We suggest you install `conda` using the `miniconda` distribution, which provides a minimal starting set. You can find the official instructions for installing `miniconda` [here](https://docs.anaconda.com/miniconda/)

To install Miniconda on a remote server, follow these steps:

```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```

Following installation you can initialize `conda` for your shell with:

```
~/miniconda3/bin/conda init bash
```

After the initialization, activate the Miniconda environment by running the following command. This step only needs to be done the first time. Alternatively you can simply log out and log back in. This will update your shell with the necessary environment variables.

```
source ~/.bashrc
```