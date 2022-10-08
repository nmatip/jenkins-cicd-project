1) Jenkins/Maven/Ansible
    - Create an Amazon Linux 2 VM instance and call it "jenkins-maven-ansible"
    - Instance type: t2.medium
    - Security Group (Open): 8080, 9100 and 22 to 0.0.0.0/0
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/awanmbandi/eagles-batch-devops-projects/blob/maven-nexus-sonarqube-jenkins-install/jenkins-install.sh
    - Launch Instance
2) SonarQube
    - Create an Create an Ubuntu 18.04 VM instance and call it "SonarQube"
    - Instance type: t2.medium
    - Security Group (Open): 9000, 9100 and 22 to 0.0.0.0/0
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/awanmbandi/eagles-batch-devops-projects/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
    - Launch Instance
3) Nexus
    - Create an Amazon Linux 2 VM instance and call it "Nexus"
    - Instance type: t2.medium
    - Security Group (Open): 8081, 9100 and 22 to 0.0.0.0/0
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/awanmbandi/eagles-batch-devops-projects/blob/maven-nexus-sonarqube-jenkins-install/nexus-install.sh
From Jespo Mbwoge to Everyone 09:42 PM (Disregard user data)
4) EC2 (Dev/Stage/Prod)
    - Create 3 Amazon Linux 2 VM instance and call them (Names: Dev-Env, Stage-Env and Prod-Env)
    - Instance type: t2.micro
    - Security Group (Open): 8080, 9100 and 22 to 0.0.0.0/0
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/awanmbandi/eagles-batch-devops-projects/blob/maven-nexus-sonarqube-jenkins-install/nexus-install.sh
	
From Jespo Mbwoge to Everyone 09:48 PM
5) Prometheus
    - Create an Ubuntu 20.04 VM instance and call it "Prometheus"
    - Instance type: t2.micro
    - Security Group (Open): 9090 and 22 to 0.0.0.0/0
    - Key pair: Select or create a new keypair
    - Launch Instance
6) Grafana
    - Create an Ubuntu 20.04 VM instance and call it "Grafana"
    - Instance type: t2.micro
    - Security Group (Open): 3000 and 22 to 0.0.0.0/0
    - Key pair: Select or create a new keypair
    - Launch Instance
	
From Jespo Mbwoge to Everyone 09:57 PM
7) Slack
    - Go to the bellow Workspace and create a Private Slack Channel and name it "yourfirstname-jenkins-cicd-pipeline-alerts"
    - Link: https://join.slack.com/t/jjtech-eagles-cicd/shared_invite/zt-1go3k7pz7-uSy3D4ai3Pb7KJk2G1sc1g
create a Private Slack Channel and name it "yourfirstname-jenkins-cicd-pipeline-alerts"
From Jespo Mbwoge to Everyone 10:07 PM
8) Go to GitHub
    - Login to your GitHub Account
    - Create a Repository called "Jenkins-CICD-Project"
    - Clone the Repository in the "Repository" directory/folder in your local
    - Download the code in in this repository "Main branch": https://github.com/awanmbandi/eagles-batch-devops-projects.git
    - Unzip the code/zipped file
    - Copy and Paste everything from the zipped file into the repository you cloned in your local
    - Add the code to git, commit and push it to your upstream branch "main or master"
    - Confirm that the code exist on GitHub
	
From Jespo Mbwoge to Everyone 10:21 PM
9) Configure Promitheus
    - Login/SSH to your Prometheus Server
    - Clone the following repository: https://github.com/awanmbandi/eagles-batch-devops-projects.git
    - Change directory to "eagles-batch-devops-projects"
    - Swtitch to the "prometheus-and-grafana" git branch
    - Run: ./install-prometheus.sh
    - Confirm the status shows "Active (running)"
    - Exit
	
10) Configure Grafana
    - Login/SSH to your Grafana Server
    - Clone the following repository: https://github.com/awanmbandi/eagles-batch-devops-projects.git
    - Change directory to "eagles-batch-devops-projects"
    - Swtitch to the "prometheus-and-grafana" git branch
    - Run: ls or ll  (to confirm you have the branch files)
    - Run: ./install-grafana.sh
    - Confirm the status shows "Active (running)"
    - sudo systemctl start grafana-server
    - sudo systemctl status grafana-server
    - sudo systemctl enable grafana-server
    - Exit
	
11) Configure The "Node Exporter" accross the "Dev", "Stage" and "Prod" instances including your "Pipeline Infra"
    - Login/SSH into the "Dev-Env", "Stage-Env" and "Prod-Env" VM instance
    - Perform the following operations on all of them
    - Install git by running: sudo yum install git -y
    - Clone the following repository: https://github.com/awanmbandi/eagles-batch-devops-projects.git
    - Change directory to "eagles-batch-devops-projects"
    - Swtitch to the "prometheus-and-grafana" git branch
    - Run: ls or ll  (to confirm you have the branch files)
    - Run: ./install-node-exporter.sh
    - Confirm the status shows "Active (running)"
    - Access the Node Exporters running on port "9100", open your browser and run the below
        - Dev-EnvPublicIPaddress:9100   (Confirm this page is accessible)
        - Stage-EnvPublicIPaddress:9100   (Confirm this page is accessible)
        - Prod-EnvPublicIPaddress:9100   (Confirm this page is accessible)
    - Exit
	
12) Configure The "Node Exporter" on the "Jenkins-Maven-Ansible", "Nexus" and "SonarQube" instances
    - Login/SSH into the "Jenkins-Maven-Ansible", "Nexus" and "SonarQube" VM instance
    - Perform the following operations on all of them
    - Install git by running: sudo yum install git -y    (The SonarQube server already has git)
    - Clone the following repository: https://github.com/awanmbandi/eagles-batch-devops-projects.git
    - Change directory to "eagles-batch-devops-projects"
    - Swtitch to the "prometheus-and-grafana" git branch
    - Run: ls or ll  (to confirm you have the branch files including "install-node-exporter.sh")
    - Run: ./install-node-exporter.sh
    - Make sure the status shows "Active (running)"
    - Access the Node Exporters running on port "9100", open your browser and run the below
        - Jenkins-Maven-AnsiblePublicIPaddress:9100   (Confirm the pages are accessible)
        - NexusPublicIPaddress:9100
        - SonarQubePublicIPaddress:9100
		
13) Update Your Jenkins file with your Slack Channel Name
    - Go back to your local, open your "Jenkins-CICD-Project" repo/folder/directory on VSCODE
    - Open your "Jenkinsfile"
    - Update the slack channel name on line "97"
    - Change name from "jenkins-cicd-pipeline-alerts" to yours
    - Add the changes to git, commit and push to GitHub
    - Confirm the changes reflects on GitHub
	
14) Once you confirm the above requirements have been fully served and Tested
    - Go ahead and Stop all your Instances
    - Please do not Terminate