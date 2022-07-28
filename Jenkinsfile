pipeline {
  agent {
    worker {
      // inheritFrom {
      //   id = "kubernetes-pipeline"
      // }
      // yaml '''
      //   apiVersion: v1
      //   kind: Pod
      //   spec:
      //     containers:
      //     - name: docker
      //       image: docker:latest
      //       command:
      //       - cat
      //       tty: true
      //       volumeMounts:
      //        - mountPath: /var/run/docker.sock
      //          name: docker-sock
      //     volumes:
      //     - name: docker-sock
      //       hostPath:
      //         path: /var/run/docker.sock    
      //   '''
    }
  }
  stages {
    stage('Clone') {
      steps {
        container('docker') {
          git branch: 'master', changelog: false, poll: false, url: 'https://github.com/Saif-Uz-Zaman/react-docker.git'
          sh 'ls'
          sh 'docker -v'
          sh 'docker ps'
          sh 'docker build -t ss69261/testing-image:latest .'
        }
      }
    }
    stage('Build-Docker-Image') {
      steps {
        container('docker') {
          sh 'docker -v'
          sh 'docker ps'
          sh 'docker build -t ss69261/testing-image:latest .'
        }
      }
    }
    stage('Login-Into-Docker') {
      steps {
        container('docker') {
          sh 'docker login -u <docker_username> -p <docker_password>'
      }
    }
    }
     stage('Push-Images-Docker-to-DockerHub') {
      steps {
        container('docker') {
          sh 'docker push ss69261/testing-image:latest'
      }
    }
     }
  }
    post {
      always {
        container('docker') {
          sh 'docker logout'
      }
      }
    }
}