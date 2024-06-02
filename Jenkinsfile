pipeline {
    agent any
    stages {
        stage("GIT CHECKOUIT") {
            steps {
                echo "git checkout started"
                git url: "https://github.com/Akil2020/addressbook-cicd-project"
            }
        }
        stage("COMPILE") {
            steps {
                echo "Compiling the Code - Maven"
                sh "mvn compile"
            }
        }  
        stage("TEST") {
            steps {
                echo "Testing the Code - Maven"
                sh "mvn test"
            }
        }
        stage("QA") {
            steps {
                sh "mvn checkstyle:checkstyle"
                echo "QA for the Code - Maven"
                recordIssues tool: checkStyle(pattern: 'target/checkstyle-result.xml')
            }
        }
        stage("PACKAGE") {
            steps {
                echo "Packaging the Code - Maven"
                sh "mvn package"
            }
        }
        stage("DEPLOY") {
            steps {
                echo "Deploy the package - Maven"
                sh "sudo cp /var/lib/jenkins/workspace/addressbook/target/addressbook.war /opt/apache-tomcat-8.5.100/webapps"
            }
        }
    }
}
