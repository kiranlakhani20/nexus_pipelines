pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                
                sh """#!/bin/bash
                 echo "Testing" >"servicenow_${env.BUILD_ID}.jar"
         """
                
                 script {
                echo "TESTNNG"
                
                 }
                
                     
            }
        }
        stage('test') {
            steps {
                script {
                echo 'Hello World'
                }
               
            }
        }
       stage('upload') {
            steps {
                
                script {
                echo 'Hello World'
                
                
                // Get Jenkins environment variables
                    def jenkinsInstanceName = env.NODE_NAME
                    def pipelineName = env.JOB_NAME
                    def buildId = env.BUILD_ID
                    
                    // Remove characters not allowed in Nexus tag
                    jenkinsInstanceName = jenkinsInstanceName.replaceAll('[^a-zA-Z0-9]', '_')
                    pipelineName = pipelineName.replaceAll('[^a-zA-Z0-9]', '_')
                    
                    // Create tag name
                    def tagName = "${jenkinsInstanceName}_${pipelineName}_${buildId}"
                    
                    // Create tag in Nexus
                    
                   // createTag nexusInstanceId: 'nexus', tagName: tagName
                    
                    createTag nexusInstanceId: 'nexus', tagAttributesJson: '''{"repos": ["maven-releases"] }''', tagName: tagName
             
             
             nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'servicenow_'+env.BUILD_ID+".jar"]], mavenCoordinate: [artifactId: 'servicenow', groupId: 'com.servicenow', packaging: 'jar', version: '1.1']]], tagName: tagName
             
                                  
                    
                }
            }
        }
    }
}
