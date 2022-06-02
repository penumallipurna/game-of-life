node('jdk8') {
    stage('SourceCode') {
        git branch: 'sprint2_develop', url: 'https://github.com/penumallipurna/game-of-life.git'
    }
    stage('Package') {
        sh 'mvn package'
    }
    stage('Archiving and Test Results') {
        junit '**/surefire-reports/*.xml'
        archiveArtifacts artifacts: '**/*.war', followSymlinks: false
    }
}