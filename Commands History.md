1. To Create a new AWS EC2 Instance
    * Always make sure to make the keypair accessible in the right way 
        * chmod 400 keypair.pem
    * Always make sure to specify the right connection and security settings and 
    explicitly define the ports that are to be kept open
        * 

2. To connect to the newly created EC2 instance from terminal:
    * ssh -i ec2_2.pem ec2-user@ec2-18-134-142-221.eu-west-2.compute.amazonaws.com
        * ssh -> connection protocol
        * i -> Identity 
        * anyfile.pem -> KeyPair file to confirm the identity for EC2 instance access
        * ec2-user -> User name, standard for AWS Linux OS
        * long address -> IPv4 address for the instance

3. Get mini-conda installer file, unzip it to locally install mini-conda in the ~/miniconda folder,
and add the mini-conda path to the ~/.bashrc file
    * wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh 
    
    # For Daniel's project
    # wget https://repo.continuum.io/miniconda/Miniconda3-py37_4.9.2-Linux-x86_64.sh -O ~/miniconda.sh

    * bash ~/miniconda.sh -b -p ~/miniconda 
    * echo "PATH=$PATH:$HOME/miniconda/bin" >> ~/.bashrc 
    * source ~/.bashrc

4. Create a new data directory and transfer the local drive contents to AWS EC2 storage 
    * mkdir data
        * make a new directory in the home folder
    * cd data
        * change the current working directory to the newly created data directory
    * scp -r -i ec2_2.pem *.* ec2-user@ec2-18-134-142-221.eu-west-2.compute.amazonaws.com:/home/ec2-user/data
        * scp -> Mandatory command
        * -r -> to signify recursive behaviour
        * -i -> Identity 
        * anyfile.pem -> KeyPair file to confirm the identity for EC2 instance access
        * *.* -> To copy all the contents of the local drive
        * ec2-user -> User name, standard for AWS Linux OS
        * long address -> IPv4 address for the instance
        * :/home/ec2-user/data -> data folder on the EC2 instance where the local files will be transferred

5. pip install -r requirements.txt
    * To install the required libraries in the current environment

6. Alternately, to clone any git repo:
    * git clone https://github.com/repo.git
    * cd appropriate_folder

7. Run any command needed.

8. Once the SSH session in the terminal is stopped, the app will stop working. To make it accessible at all times, use TMUX. It detaches the apps from the terminal and keeps them running in the background.
    * Stop the previous SSH session in the terminal
    * Install tmux
        * sudo yum install tmux 
        OR
        * sudo apt-get install tmux
        OR
        * brew install tmux (?)
    * Create TMUX session by typing 
        * tmux new -s StreamSession
    * Run streamlit app in the tmux session
        * streamlit run streamlit.py
    * Press Ctrl+B and then D to detach the session.
    * The SSH session can now be closed.
    * To reattach to the same session, re-open the SSH shell (whenever wanted, even hours later) and type:
        * tmux reattach -t StreamSession

9. If the app is not hosting on the 8501 port, we can check the apps consuming any ports by:
    * ps aux | grep streamlit
    * kill -9 process_id
