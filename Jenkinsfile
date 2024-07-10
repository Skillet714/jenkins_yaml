import org.yaml.snakeyaml.Yaml

pipeline {
    agent any
    
    stages {
        stage('1') {
            steps {
                script {
                    // def yamlFile = new File('"Z:/1/1.yaml"')
                    // def yamlObject = new Yaml().load(yamlFile)
                    // echo "${yamlObject}"

                    def yaml1 = new Yaml()
                    def inputStream1 = new FileInputStream('Z:/1/1.yaml')
                    def yamldata1 = yaml1.load(inputStream1)
                    println("Файл 1")
                    println yamldata1

                    def yaml2 = new Yaml()
                    def inputStream2 = new FileInputStream('Z:/1/2.yaml')
                    def yamldata2 = yaml2.load(inputStream2)
                    println("Файл 2")
                    println yamldata2

                    def yaml3 = new Yaml()
                    def data = []

                    for ( i in yamldata1 ) {
                        // println i.key
                        def keyYaml = i.key
                        if ( keyYaml in yamldata2 ) {
                            def value = yamldata2."${keyYaml}"
                            //println ("${keyYaml}=${value}")
                            println ("${keyYaml}=")
                            for ( o in yamldata2."${keyYaml}" ) {
                            // println ("${o}=${value}")
                                
                                def value3 = "${o}"
                                println value3
                                
                            }
                        }
                        else {
                            //def value = yamldata1."${keyYaml}"
                            //println ("${keyYaml}=${value}")
                            println ("${keyYaml}")
                            for ( o in yamldata1."${keyYaml}" ) {
                                for ( u in yamldata1."${keyYaml}"."${o.key}") {
                                    def value3 = "${u} пустое значение 2"
                                    println value3
                                }
                            // println ("${o}=${value}")
                                // def value3 = "${o.key} пустое значение 3"
                                // println value3
                            }
                            //println ("${keyYaml}: # не_найдено_значение")
                        }
                        // println keyYaml
                        
                    }
                }
            }
        }
    }
}
