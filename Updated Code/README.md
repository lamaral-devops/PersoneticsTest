# These were the changes and fixes made to the code:

1. The "inventory" file had the wrong "ansible_host" parameter, so it was necessary to put the correct IP address
to deploy correctly, both Jenkins and minikube, using the provided playbooks

2. The Dockerfile_Jenkins_Master underwent the following changes:
   - The RUN commands were grouped into a single instruction to reduce the number of layers in the Docker image and improve the efficiency of the build.
   - In the RUN command where the docker group is being created and the Jenkins user is being added, I added a check to see if the docker group already exists.
   - I also added a check to see if the version of the plugin being installed is compatible with the Jenkins version.
   - A permissions check of the "jenkins_master_casc.yaml" file was added before its copy to "/var/jenkins_home/casc.yaml".

3. The path "/usr/local/bin/docker:/usr/local/bin/docker" was added to the docker-compose volumes.

4. It was also necessary to change the permissions of the pem keys using the command "chmod 400 file-name" and move them into the "deployment" folder.

After these changes, it was only necessary to run the command "ansible-playbook -i inventory deploy_jenkins" and "ansible-playbook -i inventory deploy_minikube", and both servers were up and running.

Unfortunately, I was not able to solve some Jenkins plugin problems in time, and the Jenkinsfile was not successfully executed. Attached is a screenshot of the initial Jenkins screen, proving my access.

Link to the github repository: https://github.com/lamaral-devops/PersoneticsTest