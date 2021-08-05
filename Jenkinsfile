pipeline{
    agent {
        docker {
            image 'allbears/jenkins-android:1.0.1' //① 这里的 image 参数是用来下载 allbears/jenkins-android:1.0.1 Docker 镜像（如果你的机器还没下载过它）
            //并将该镜像作为单独的容器运行。你也可以用 `docker pull allbears/jenkins-android:1.0.1` 命令预先将镜像下载到你的宿主机上。
        }
    }
    stages {
        stage('Build'){
             steps {
                sh './gradlew clean && rm -rf ./app/build/' //②这里的 sh step 是在编译前进行一些准备动作，对你的工程环境进行清理，确保工作时，编译工程环境干净。
                sh './gradlew assembleRelease'  //③ 这里的 sh step 运行的是一个 gradle 构建 release 包的命令。
             }
        }
          stage('UnitTest'){  //这里增加了一个 UnitTest 的 stage，之后会出现在 Jenkins UI 上。
             steps {
                sh './gradlew test' //里的 sh step 运行的是一个 gradle 执行单元测试的命令，该命令执行之后会进行单元测试。  
             }
        }
          stage('Archive') {  //`stage('Archive')` 这里定义了一个名为 Archive 的 stage，之后会出现在 Jenkins UI 上。  
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/**/*.apk'， fingerprint: true    //`archiveArtifacts` 这一行执行了一个归档构建产物的操作，执行完这步操作后我们将在任务界面看见我们执行成功后的产物输出。  
            }
        }

    }

}