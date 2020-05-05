pipeline {
    agent none
    options {
        timeout(time: 40, unit: 'MINUTES')
        ansiColor('xterm')
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
    }
    parameters {
        string(name: 'component', defaultValue: '<service>', trim: true, description: 'Specify service component name to deploy. This name lines up with the applications in neptune deploy: https://github.com/AudaxHealthInc/neptune-deploy/tree/master/applications')
        string(name: 'version', defaultValue: '<version>', trim: true, description: 'Specify version of service to deploy')
        string(name: 'tenant', defaultValue: '', trim: true, description: 'The tenant name to deploy to. Please ONLY provide the tenant name, not DNS entry. For example: prod')
        string(name: 'releaseticket', defaultValue: 'REL-123', trim: true, description: 'Release ticket for this deployment, e.g. REL-123')
        string(name: 'extra_vars', defaultValue: '', trim: true, description: 'JSON dict string containing extra variables, which will be passed to Ansible.  For example: {"foo":"bar","biff":"brap"}')
        booleanParam(name: 'dry_run', defaultValue: true, description: 'When selected, build will be a dry run')
    }
    stages {
        stage('Collect parameters') {
            // Only be dynamic if tenant not already entered.  Indicates first run on a new branch
            when { not { expression { params.tenant } } }
            agent none
            steps {
                script {
                    params = input(message: 'Component Deploy Parameters',
                        id: 'parameters',
                        parameters: [
                            string(name: 'component', defaultValue: '<service>', trim: true, description: 'Specify service component name to deploy'),
                            string(name: 'version', defaultValue: '<version>', trim: true, description: 'Specify version of service to deploy'),
                            string(name: 'tenant', defaultValue: '', trim: true, description: 'The tenant name to deploy to'),
                            string(name: 'releaseticket', defaultValue: 'REL-123', trim: true, description: 'Release ticket for this deployment, e.g. REL-123'),
                            string(name: 'extra_vars', defaultValue: '', trim: true, description: 'JSON dict string containing extra variables, which will be passed to Ansible.  For example: {"foo":"bar","biff":"brap"}'),
                            booleanParam(name: 'dry_run', defaultValue: true, description: 'When selected, build will be a dry run')
                        ])
                }
            }
        }
    }
}

