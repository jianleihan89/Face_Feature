# The detailed steps for running the face_feature project

platform：windows11 based on amd64

environment：docker

IDE：vscode

Python：3.9.5

## Step 1: Configure the environment for installing Docker

Since installing Docker on Windows depends on Hyper-V and the Windows Subsystem for Linux (WSL), you should first install WSL. For reference, see https://learn.microsoft.com/zh-cn/windows/wsl/install. However, since there is no Hyper-V option in Win11, you can follow these steps: Create a new blank document on your desktop, copy the content below into it, then change the .txt file extension to a .bat extension. Finally, right-click and run it as an administrator.

```-bash
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL
pause
```

The above execution process will display the running process in the terminal, and you need to restart your computer after completion.

Finally, in the Windows search bar, type "Enable or Disable Windows Features," click to open its panel, as shown below. Check the box for Hyper-V. This completes the prerequisite steps for installing Docker on Windows 11.

## Step 2: Install Docker

Directly download the corresponding version from the official website (https://www.docker.com/). You should select the version that matches your computer. Follow the default installation settings. With this, the Docker installation is complete.

![download docker for windows](figures\fig1.png)

## Step 3: Pull Docker Image

After completing step 2, there will be a Docker icon on the desktop. Double-click to open it, and you will need to log in with your account. Follow the software's guidance to complete this step. You need to register an account and log in. Then, open the terminal in the software interface as shown below.

![open the docker](figures\fig2.png)

Enter `docker version` in the terminal, and the following information will appear. If it does not, docker has not been installed successfully and needs to be reinstalled.

![docker version](figures\fig3.png)

Next, you can pull the docker image. In the terminal, enter `docker run -it --rm algebr/openface:latest`, and the following result will appear.

![docker run](figures\fig4.png)

Subsequently, you will be redirected to a new container.

![continer](figures\fig5.png)

You can open a new terminal in the Docker software interface and enter `docker ps`. The container ID (c9891d21c055) will appear, which will be needed later. With this, the Docker image pull is complete.

![continer id](figures\fig6.png)

## Step 4: Run the script feature_extract.py

You can run it in VS Code, which can be downloaded and installed from the official website (https://code.visualstudio.com/). After that, simply open the VSCode software, open a folder to serve as the root directory for pulling project files. In the example, **C:\Users\Yuuuu** is the directory (you can change this according to your needs), then in the VSCode interface, use the shortcut key **CTRL + J** to summon the terminal. In the terminal, enter the command `git clone https://gitee.com/zhikai-22/face_feature.git`, and you can pull the repository locally.

Next, make the following modifications to the script file `feature_extract.py`.

```-python
DOCKER_ID = 'c9891d21c055' # replace with your own container ID
folder = r'C:\Users\Yuuuu\face_feature\video' # replace with your own path
output_dir = r'C:\Users\Yuuuu\face_feature\output' # replace with your own path
```

Then, in the VSCode interface, use the shortcut key combination CTRL + Shift + P to select a Python interpreter greater than python3.6. You need select according to your preference, and this example uses python3.9.

![vscode interpreter](figures\fig7.png)

Finally, run the script file `feature_extract.py` in the terminal, and you will get the following results. There are two result files in C:\Users\Yuuuu\face_feature\output, namely 2015-10-15-15-14.csv and 2015-10-15-15-14.hog.

![error](figures\fig9.png)