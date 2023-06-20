https://dev.to/jmprobst/jenkins-build-a-private-github-repo-5489
https://www.techbeatly.com/ultimate-guide-to-deploying-a-jenkins-multinode-cluster-on-aws-with-linux-and-windows-slave-nodes/



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


* Master
    sudo apt update -y
    sudo apt-get install fontconfig openjdk-11-jre -y
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt update -y
    sudo apt install jenkins -y
    
    + Adding the node.
        Open Manage jenkins
        Nodes and Clouds
        Add New Node
        Home Location /home/ubuntu
        Ip must be Public-IP
        


    



* Slave

    sudo apt update -y
    sudo apt-get install fontconfig openjdk-11-jre -y
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt update -y
    sudo apt install jenkins -y
    ssh-keygen
    Add id_rsa.pub to authorized keys
    Copy the id_rsa to Jenkins Credentials -- Username with Private Key



- https://towardsdatascience.com/create-your-first-ci-cd-pipeline-with-jenkins-and-github-6aefe21c9240
- https://devopscube.com/jenkins-2-tutorials-getting-started-guide/
- https://devopscube.com/setup-slaves-on-jenkins-2/
- https://itnext.io/jenkins-running-workers-in-kubernetes-and-docker-images-build-83299a10f3ca
- https://faun.pub/devops-create-your-first-ci-cd-pipeline-ed054ba1404f
- https://chathura-siriwardhana.medium.com/step-by-step-guide-to-add-jenkins-slave-nodes-f2e756c8849e
- https://www-softwaretestinghelp-com.cdn.ampproject.org/v/s/www.softwaretestinghelp.com/distributed-builds-jenkins-master-slave/amp/?amp_gsa=1&amp_js_v=a9&usqp=mq331AQIKAGwASCAAgM%3D#amp_tf=From%20%251%24s&aoh=16677230725211&csi=0&referrer=https%3A%2F%2Fwww.google.com&ampshare=https%3A%2F%2Fwww.softwaretestinghelp.com%2Fdistributed-builds-jenkins-master-slave%2F
- https://blog.kipchirchirlangat.com/series/jenkins-guide-django
- https://django-jenkins.readthedocs.io/en/latest/
- https://skamalakannan.dev/posts/jenkins-pipeline-python/
- https://semaphoreci.com/blog/python-continuous-integration-continuous-delivery
- https://github.com/semaphoreci-demos/semaphore-demo-python-django
- https://cloudaffaire.com/how-to-integrate-github-repository-with-jenkins/
- https://gitlab.com/daresoremi/polling/-/blob/master/Jenkinsfile

