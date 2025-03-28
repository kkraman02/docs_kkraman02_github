---
title: Jenkins
date: 2025-03-28 20:30:00
categories: Jenkins
tags: Jenkins
---



Jenkins is a popular open-source framework. It helps developers to automate the software development, testing, and deployment  their software products, for an example Embedded Linux Yocto development.



## Installing Jenkins

- In prior installing Jenkins, [install Java](https://www.jenkins.io/doc/book/installing/linux/#installation-of-java) because it Jenkins requires Java.

- Refer to [here](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu) for installing Jenkins on Ubuntu host. Choose the LTS release instead of weekly release in order setup more stable environment.



## Start Jenkins

Enable the Jenkins service to start at boot with the command

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

Check the status of the Jenkins service using the command

```bash
sudo systemctl status jenkins
```

If everything has been set up correctly, you should see an output like this

```bash
Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
Active: active (running) since Tue 2018-11-13 16:19:01 +03; 4min 57s ago
```



## Post-installation Setup

- This setup wizard takes you through a few quick "one-off" steps to unlock Jenkins, customize it with plugins and create the first administrator user through which you can continue accessing Jenkins.

- Refer to [here](https://www.jenkins.io/doc/book/installing/linux/#setup-wizard) to get more detailed information.



## Start a New Job

- Dashboard -> **click** New Item -> 
- Name your job item and choose the job type.
- For beginner it's recommended to go with **Freestyle project**. It offers you the shell environment to design the job workflow.
- Advanced users go with **Pipeline**. It offers you to write down your workflow in groovy format. Hence, you will get more control.



## Defining Pipeline Using Groovy Script

- Dashboard -> Job Name -> Configuration ->

  ```groovy
  pipeline {
      agent any
  
      environment {
          YOCTO_DIR = "/media/raman/development/jenkins_x86_yocto"
          POKY_REPO = "git://git.yoctoproject.org/poky"
          POKY_BRANCH = "kirkstone"
      }
  
      stages {
          stage('Checkout Yocto') {
              steps {
                  sh """
                      mkdir -p $YOCTO_DIR
                      cd $YOCTO_DIR
                      if [ ! -d poky ]; then
                          git clone -b $POKY_BRANCH $POKY_REPO
                      fi
                  """
              }
          }
  
          stage('Setup Build Environment') {
              steps {
                  sh """
                      cd $YOCTO_DIR/poky
                      bash -c 'source oe-init-build-env build && sed -i "s/^MACHINE ?=.*/MACHINE ??= \\"qemux86-64\\"/" conf/local.conf'
                  """
              }
          }
  
          stage('Build') {
              steps {
                  sh """
                      cd $YOCTO_DIR/poky
                      bash -c 'source oe-init-build-env build && bitbake core-image-minimal'
                  """
              }
          }
  
          stage('Archive Artifacts') {
              steps {
                  sh """
                      mkdir -p artifacts
                      cp -r $YOCTO_DIR/poky/build/tmp/deploy/images/qemux86-64 ./artifacts/
                  """
                  archiveArtifacts artifacts: "artifacts/qemux86-64/**/*", fingerprint: true
              }
          }
      }
  
      post {
          failure {
              echo 'Build failed!'
          }
          success {
              echo 'Build completed successfully!'
          }
      }
  }
  
  ```



## Start the First Build of Your Job

- Dashboard -> Job Name -> **click** Build Now.
- Dashboard -> Job Name -> **click** build number(#1) -> Console Output(you can monitor/see the build status).



## Make Your Jenkins Accessible Over The Network

Open the Jenkins default config file.

```bash
sudo nano /etc/default/jenkins
```

Make sure HTTP HOST is set to `HTTP_HOST=0.0.0.0`

Tell Jenkins to listen on all network interfaces.

```bash
JENKINS_ARGS="--webroot=/var/cache/$NAME/war --httpPort=$HTTP_PORT"
<!-- Change the above line as shown below --!>
JENKINS_ARGS="--webroot=/var/cache/$NAME/war --httpPort=$HTTP_PORT --httpListenAddress=0.0.0.0"
```

Save and close the config file.

Restart Jenkins.

```bash
sudo systemctl restart jenkins
```

Allow firewall access.

```bash
sudo ufw allow 8080
sudo ufw status
```

Get the system IP.

```bash
hostname -I

Output:
172.30.70.51
```

You should now be able to access your Jenkins from other machines using your server’s IP address.

```bash
http://172.30.70.51:8080/
```

