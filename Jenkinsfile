node("mavenwithnexus") {
  checkout scm

  def canaryPromptMessage = 'Would you like to do Canary or Normal Release ?'

  def isCanary =  input(message: canaryPromptMessage, ok: 'Yes',
    parameters: [booleanParam(defaultValue: false,
    description: 'If you want to do Canary Deployment press Yes', name:'Yes?')])

  if(isCanary) {

    stage("Test") {
      sh "mvn -B  test"
    }

    stage("Deploy") {
        sh "mvn  -DskipTests clean -Pcanary fabric8:deploy"
    }
  }else{

    stage("Test") {
      sh "mvn -B  test"
    }

    stage("Deploy") {
        sh "mvn  -DskipTests clean fabric8:deploy"
    }
  }

}
