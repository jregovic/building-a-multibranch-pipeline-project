pipeline {
    agent any
    environment {
        CI = 'true'
    }
    def changelogString = gitChangelog returnType: 'STRING',
  from: [type: 'REF', value: 'git-changelog-1.50'],
  to: [type: 'REF', value: 'master'],
  template: """
  <h1> Git Changelog changelog </h1>

<p>
Changelog of Git Changelog.
</p>

{{#tags}}
<h2> {{name}} </h2>
 {{#issues}}
  {{#hasIssue}}
   {{#hasLink}}
<h2> {{name}} <a href="{{link}}">{{issue}}</a> {{title}} </h2>
   {{/hasLink}}
   {{^hasLink}}
<h2> {{name}} {{issue}} {{title}} </h2>
   {{/hasLink}}
  {{/hasIssue}}
  {{^hasIssue}}
<h2> {{name}} </h2>
  {{/hasIssue}}


   {{#commits}}
<a href="https://github.com/tomasbjerre/git-changelog-lib/commit/{{hash}}">{{hash}}</a> {{authorName}} <i>{{commitTime}}</i>
<p>
<h3>{{{messageTitle}}}</h3>

{{#messageBodyItems}}
 <li> {{.}}</li> 
{{/messageBodyItems}}
</p>


  {{/commits}}

 {{/issues}}
{{/tags}}
  """
    stages {
        stage('Build') {
            steps {
              echo changelogString 
            }
        }
        stage('Test') {
            steps {
               echo 'test' 
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
pipeline {
    agent any
    environment {
        CI = 'true'
    }
    def changelogString = gitChangelog returnType: 'STRING'
    stages {
        stage('Build') {
            steps {
              echo changelogString 
            }
        }
        stage('Test') {
            steps {
               echo 'test' 
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
