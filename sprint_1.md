Creating Jenkins server in EC2



Configuring Jenkins server
Sudo apt update
sudo apt install -y openjdk-11-jdk
# Verify installation    →   java -version







Add Jenkins repository to your EC2
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

→ Add Screenshot

Update your package list again to include the new repository:
Sudo apt update


Installing Jenkins	

sudo apt install -y jenkins







Start and Enable the Jenkins Service

Sudo systemctl enable jenkins
Sudo systemctl start jenkins

Check the status to ensure it is running correctly:
Sudo systemctl status jenkins




Configuring Jenkins via the Web Interface

Open a web browser and navigate to http://<Public_IPv4_Address>:8080.


You will be prompted to unlock Jenkins with an initial admin password. Retrieve this password from the instance's log file using the following command in your SSH terminal: 
sudo cat /var/lib/jenkins/secrets/initialAdminPassword







Installing the Plugins








Creating the user admin



Jenkins Server is Up and Running successfully




