def my_parameters(a,b) {
    sum = a+b
    println "Sum of $a and $b is ${sum}"
}


pipeline {
    agent {
        label 'slave1'
    }
    stages {
        stage('Working with conditions') {
            steps {
                script {
                    my_parameters(1.2,5.7)

                    }
                    
                    
                }
            }
        }
    }
