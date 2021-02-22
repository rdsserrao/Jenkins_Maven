pipeline {
    agent any
            parameters {
                string(name: 'Imagem', defaultValue: 'jenkins1', description: 'Nome da imagem')
                string(name: 'Contentor', defaultValue: 'cont1', description: 'Nome do contentor')
                string(name: 'Porta', defaultValue: '3000', description: 'Número da porta')
            }
            stages {
                stage ('Criar Dependências') {
                    tools {
                        jdk 'JDK11'
	                    maven 'Maven3'
                    }
                    steps {
                        withMaven(maven: 'Maven3', jdk: 'JDK11') {
                        sh 'mvn clean package'
                        }
                    }         
                }
                stage ('Criar Imagem') {
                    steps {
                        sh 'docker build -t "${Imagem}" .'
                    }   
                } 
                stage ('Criar Contentor') {
                    steps {
                        sh 'docker rm -f "${Contentor}"'
                        sh 'docker run -p "${Porta}":8080 -d --name "${Contentor}" "${Imagem}"'
                    }   
                }
            }
}