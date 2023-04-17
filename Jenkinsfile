pipeline{

	agent any

		stages{

			stage('Checkout'){

					steps{

						git branch: "main", url: 'https://github.com/EegaRamakrishna/allergyservice.git'

						}

					}

			stage('Build'){

					steps{

						sh 'chmod a+x mvnw'

						sh './mvnw clean package -DskipTests=true'

						}

					post{

						always{

							archiveArtifacts 'target/*.jar'

							}

						}

				}

			stage(DockerBuild) {

						steps {

							sh 'docker build -t eegaramakrishna/g1-allergy-service:latest .'

							}

						}

			stage('Login') {

					steps {

						sh 'echo @Krishna8th | docker login -u eegaramakrishna --password-stdin'

						}

					}

			stage('Push') {

					steps {

						sh 'docker push eegaramakrishna/g1-allergy-service'

						}
	
					}
				}

		post {

			always {

				sh 'docker logout'

				}

			}

}
