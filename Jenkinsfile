import groovy.json.JsonSlurper

stage 'Verify'
node {
  env.LC_ALL="en_US.UTF-8"
  env.PATH = "/opt/chefdk/bin:${env.PATH}"

  def phases = phases_for('verify')
  checkout scm
  sh('chef exec rake verify')
  input message: 'Accept?', parameters: [[$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Accepting will publish the cookbook to the Chef Server', name: 'Accept']]
}

stage 'build'
node {
  env.LC_ALL="en_US.UTF-8"
  env.PATH = "/opt/chefdk/bin:${env.PATH}"

  def phases = phases_for('build')
}

stage 'accept'

node {
  env.LC_ALL="en_US.UTF-8"
  env.PATH = "/opt/chefdk/bin:${env.PATH}"

  def phases = phases_for('accept')
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
