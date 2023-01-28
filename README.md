# Remote Development using SSH

## Set Up Windows OS Server

### SSH Server

Here I set up a Windows OS server as a remote SSH host. 
Details on how to setup a ssh client on Windows can be found [here](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui).


### Router
SSH server requires fixed IP address. 
Usually in home internet, the router randomly assign an IP address to the connected device. 
If the device is off and on again, the IP address may be different.

To serve as a SSH server, we can go to router home page to forward SSH login to a fixed IP address, and assign that fixed IP address to the server.

### User Name and Passcode

The server hostname is typically the IP address of the rounter, which can be found by typing "my IP address" in Google.
For my case, the server hostname is `66.90.196.221`, and the user name is set to `yangyangfu`.
The passcode is upon request.

## Connect From a Mac Client

My Macbook as a SSH client can directly connect to the Windows Server through terminal. 

- open a terminal, and type

``` 
    ssh yangyangfu@66.90.196.221
```

- follow the pompted instructions, and type the passcode when needed

However, this is approach is not convinient when we need debug resource-intensive deep learning codes that use GPUs. 
The most convinient way is to modify, debug and run remote programs but on any local computer using specific GUI, such as jupyternotebook.
Here I leverage the most recent development of Visual Studio Code to seamlessly support remote development of deep learning related tasks using my GPU-enabled Windows server at home.

### Software Requirement

Basic software are required on MacOS for this purpose:
- Visual Studio Code: [download here](https://code.visualstudio.com).

Once the VSCode is installed, the following extensions should also be installed:
- python
- Remote Development, which include Remote-SSH, Dev Container, and WSL
- Remote Explorer

### Configure Remote SSH
On MacOS, the Remote SSH extension has to be modified to connect to a Windows server. Add the following three settings to the VSCode `settings.json` file.

```json
    "remote.SSH.remotePlatform": {
        "66.90.196.221": "windows"
    },
    "remote.SSH.showLoginTerminal": true,
    "remote.SSH.useLocalServer": false,

```

Now connect to the Windows server through Remote SSH:
- click the far left bottom on a VSCode window: open a Remote Window
- then follow the promped instructions: Connect to a Host -> Add New SSH Host 

## Example

This is to show the capability of editing a Jupyter Notebook file in the remote server from local computers when the above connection is established.

After connect to the server using VSCode, 

- open remote folder in local VScode: D:\kaggle\2023\1-XXXX. This should require the passcode again.
- open the notebook file in `yfu\test_notebook.ipynb`
- select jupyter notebook kernel if needed. Here we should use `pytorch-cuda-11.8`.
- run the notebook file in the local VSCode
