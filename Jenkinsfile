pipeline {
    agent any
            tools {
	            maven 'Maven 3.6.3'
	            jdk 'Java SE Development Kit 9.0.4'
            }
            parameters {
                agent any
                string(name: 'Imagem', defaultValue: 'jenkins1', description: 'Nome da imagem')
                string(name: 'Contentor', defaultValue: 'cont1', description: 'Nome do contentor')
                string(name: 'Porta', defaultValue: '3000', description: 'Número da porta')
            }
            stages {
                stage('Clean') {
                    agent any
                    steps {
                        cleanWs()
                    }
                }
                stage ('Criar Dependências') {
                    agent any
                    steps {
                        withMaven(jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') {
                        sh 'mvn clean package'
                        }
                    }         
                }
                stage ('Criar Imagem') {
                    agent any
                    steps {
                        sh 'docker build -t "${Imagem}" .'
                    }   
                } 
                stage ('Criar Contentor') {
                    agent any
                    steps {
                        sh 'docker rm -f "${Contentor}"'
                        sh 'docker run -p "${Porta}":3000 -d --name "${Contentor}" "${Imagem}"'
                    }   
                }
            }
}