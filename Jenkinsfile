buildPlugin(
  useContainerAgent: true,
  configurations: [
    [platform: 'linux', jdk: 11],
    [platform: 'windows', jdk: 11],
])

tool:
  jfrog:
    installations:
    - name: "jfrog-cli"
      properties:
      - installSource:
          installers:
          - "releasesInstaller"

tool:
  jfrog:
    installations:
      - name: "jfrog-cli"
        properties:
          - installSource:
              installers:
                - artifactoryInstaller:
                    repository: "jfrog-cli-remote"

tool:
  jfrog:
    installations:
      - name: "jfrog-cli"
        home: "/path/to/jfrog/cli/dir/"

pipeline {
    agent any
    tools {
        jfrog 'jfrog-cli'
    }
    stages {
        stage('Testing') {
            steps {
                // Show the installed version of JFrog CLI.
                jf '-v'

                // Show the configured JFrog Platform instances.
                jf 'c show'

                // Ping Artifactory.
                jf 'rt ping'

                // Create a file and upload it to a repository named 'my-repo' in Artifactory
                sh 'touch test-file'
                jf 'rt u test-file my-repo/'

                // Publish the build-info to Artifactory.
                jf 'rt bp'

                // Download the test-file
                jf 'rt dl my-repo/test-file'
            }
        }
    }
}