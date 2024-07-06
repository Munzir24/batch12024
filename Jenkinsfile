def my_parameters(a,b) {
    Division = a/b
    println "Division of $a and $b is ${Division}"
}


pipeline {
    agent {
        label 'slave1'
    }
    stages {
        stage('Working with functions') {
            steps {
                script {
                    my_parameters(1.2,5.7)

                    }
                    
                    
                }
            }
        }
    }
