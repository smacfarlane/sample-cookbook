import groovy.json.JsonSlurper

stage 'Verify'
node {
  env.LC_ALL="en_US.UTF-8"
  env.PATH = "/opt/chefdk/bin:${env.PATH}"
  # git changelog: false, credentialsId: '', poll: false, url: 'https://github.alaska.edu/sdmacfarlane/sample-cookbook'

  def phases = phases_for('verify')
  sh("delivery job verify '${phases}' -l")
}

stage 'build'
node {
  env.LC_ALL="en_US.UTF-8"
  env.PATH = "/opt/chefdk/bin:${env.PATH}"
  # git changelog: false, credentialsId: 'jenkins-ghe-oauth', poll: false, url: 'https://github.alaska.edu/sdmacfarlane/sample-cookbook'

  def phases = phases_for('build')
  sh("delivery job build '${phases}' -l")
}

stage 'accept'

node {
  input message: 'Accept?', parameters: [[$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Accepting will publish the cookbook to the Chef Server', name: 'Accept']]

  env.LC_ALL="en_US.UTF-8"
  env.PATH = "/opt/chefdk/bin:${env.PATH}"
  # git changelog: false, credentialsId: 'jenkins-ghe-oauth', poll: false, url: 'https://github.alaska.edu/sdmacfarlane/sample-cookbook'

  def phases = phases_for('accept')
  sh("delivery job build '${phases}' -l")
}

def phases_for(String stage) {
    switch(stage) {
        case "verify":
            return "lint syntax unit"
        case "build":
            return "lint syntax unit security quality publish"
        case "accept":
            return "functional"
            return "provision deploy smoke functional"
    }
}
