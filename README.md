# Gitlab-Setup

# Pre-Requisites
    Amazon Linux Instance
    Check required dependencies
# Check required dependencies:
    systemctl status postfix
  If not in active please follow below steps:
  # Install and Configure Required Dependencies:
  1. First, start by installing the following necessary dependencies using the yum package manager as shown
  
    yum install curl policycoreutils-python openssh-server 
  2. Install Postfix service to send notification emails, and enable it to start at system boot, then check if it is up and running using following commands.
    
    yum install postfix
    systemctl start postfix
    systemctl enable postfix
    systemctl status postfix
# Gitlab Installation:
  # Add GitLab Repository and Install Package
    curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
    EXTERNAL_URL="http://54.144.17.106" yum install -y gitlab-ce
# Note: 
  If you want to change your main URL, you can configure it in the GitLab main configuration file /etc/gitlab/gitlab.rb in the external_url section. Once changed, don’t  forget to reconfigure gitlab to apply the recent changes in the configuration file using the following command.
  
    gitlab-ctl reconfigure
# Goto WebUI and check GitLab open or not
  Open portnumber 80 in security group and check in WebUI
    
    http://54.144.17.106/
  On your first visit, you’ll be redirected to a password reset screen, create a new password for your new admin account and click “Change your password”. Once you set, it will be redirected back to the login screen and login with username root and the password you set.
  
  ![image](https://user-images.githubusercontent.com/58024415/104082926-31286100-5260-11eb-9bad-7a4f1528734a.png)
# Install GitLab Runner
  Go to the project’s Settings > CI/CD and expand the Runners section and get URL and tiken
    
    sudo gitlab-runner register -n \
        --url http://54.144.17.106/ \
        --registration-token bszC6hSfL8fxaW4yQief \
        --executor shell \
        --description "shell-runner"
   Here We can you different executors, like shell, ssh, docker, kubernetes etc..,
 # Goto WebUI and check Runner
   Go to the project’s Settings > CI/CD and expand the Runners section
   Click on Expand
   
   ![image](https://user-images.githubusercontent.com/58024415/104083102-d0018d00-5261-11eb-8064-51d33e1de759.png)
