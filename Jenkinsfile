 stage('Read YAML file') {
        steps {
            script{ datas = readYaml (file: 'Jenkinsfile.yml') }
            echo datas.ear_file.deploy.toString()

        }
    }
}