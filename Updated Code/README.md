# These were the changes and fixes made to the code:

1. The "inventory" file had the wrong "ansible_host" parameter, so it was necessary to put the correct IP address
so that it was possible to deploy, both Jenkins and minikube, correctly using the provided playbooks.

- jenkins
   jenkins_master <ansible_host=54.229.22.238> ansible_user=ec2-user host_key_checking=False ansible_ssh_private_key_file=jkey.pem

- minikube
   minideploy <ansible_host=176.34.79.63> ansible_user=ec2-user host_key_checking=False ansible_ssh_private_key_file=skey.pem

2. The Dockerfile_Jenkins_Master underwent the following changes:
   - The RUN commands were grouped into a single instruction to reduce the number of layers in the Docker image and improve the efficiency of the build.
   - In the RUN command where the docker group is being created and the Jenkins user is being added, I added a check to see if the docker group already exists.
   - I also added a check to see if the version of the plugin being installed is compatible with the Jenkins version.
   - A permissions check of the "jenkins_master_casc.yaml" file was added before its copy to "/var/jenkins_home/casc.yaml".

3. The path "/usr/local/bin/docker:/usr/local/bin/docker" was added to the docker-compose volumes.

4. It was also necessary to change the permissions of the pem keys with the command "chmod 400 + <file-name>" and move them into the "deployment" folder.

After the changes, it was only necessary to run the command "ansible-playbook -i inventory deploy_jenkins" and "ansible-playbook -i inventory deploy_minikube" so that
the Jenkins server was up and running and so was minikube.

Unfortunately, I was not able to solve some Jenkins plugin problems in time, and the Jenkinsfile was not successfully executed. Attached is a screenshot of the initial Jenkins screen, proving my access.

Link to the github repository: https://github.com/lamaral-devops/PersoneticsTest