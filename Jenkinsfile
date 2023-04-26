pipeline{
  agent any
    stages{
      stage('git checkout'){
        steps{
           git branch: 'main', url: 'https://github.com/thapakrishna0111/counter-app.git'
        }
      }
      stage('UNIT Testing'){
        steps{
           sh 'mvn test'
        }
      }

    }

}
