import org.yaml.snakeyaml.Yaml

pipeline {
    agent any
    
    stages {
        stage('Создание yaml файла на основе двух других') {
            steps {
                script {
                    def yaml1 = new Yaml()
                    def inputStream1 = new FileInputStream('Z:/1/1.yaml')
                // в данном скрипте используются многострочные переменные вместо файла которые повторяют структуру yaml файла
                    // def inputStream1 = env.firstFile 
                    def yamldata1 = yaml1.load(inputStream1) // Читаем данные из первого файла
                    println("Файл 1")
                    println yamldata1

                    def yaml2 = new Yaml()
                    def inputStream2 = new FileInputStream('Z:/1/2.yaml')
                    // def inputStream2 = env.secondFile
                    def yamldata2 = yaml2.load(inputStream2) // Читаем данные из второго файла
                    println("Файл 2")
                    println yamldata2

                    for ( i in yamldata1){ // перебираем группы из первого файла
                        def iKey = i.key
                        for (u in i.value) { // перебираем ключи внутри групп из первого файла
                            
                            def testValue = u.value
                            def testKey = u.key

                            if ( iKey in yamldata2) { // Заменяем значения ключа из первого файла значением из второго
                                yamldata1."${iKey}"."${testKey}" = yamldata2."${iKey}"."${testKey}"
                            }

                            else if ( "host" in testValue ) { // Если в группе есть подгруппа, меняем значение ключа в подгруппе
                                for (p in u.value){
                                    def pKey = p.key
                                    yamldata1."${iKey}"."${testKey}"."${pKey}" = "# не_найдено_значение"
                                }
                                
                            }
                            else { // Если не нашли ключ во втором файле подставляем свое значение
                                yamldata1."${iKey}"."${testKey}" = "# не_найдено_значение"
                            }
                            
                        }
                    }
                    println("Файл 3")
                    println yamldata1
                    // sh "rm 3.yaml"
                    writeYaml file:"Z:/1/3.yaml", data: yamldata1

                    // emailext body: "123",
                    //     mimeType: 'text/plain',
                    //     attachmentsPattern: "3.yaml",
                    //     subject: "Отправка yaml",
                    //     to: 'DPPinaykin@sberbank.ru'
                }
            }
        }
    }
}
