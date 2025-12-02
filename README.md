# learning-game


kubernetes:
windows powershell(administrator mode)
cmds: 1.minikube start 1
2.docker login
3.minikube version 
4.minikube status
5.kubectl create deployment myngnix --image=ngnix 2
6. minikube status
7.kubectl get deployment
8.kubectl get pods 3
9.kubectl describe pods 4
10.kubectl scale deployment myngnix --replicas=4 5
11.kubectl get deployment 6
12.kubectl get pods 7
16.kubectl expose deployment myngnix --type=NodePort --port=80  8
15.kubectl get service myngnix or  9.1
17.kubectl service myngnix(finnaly) 9
18.kubectl port-forward service/myngnix 30088:80 10
19.in browser type 127.0.0.1:30088(ntg copy and paste the url in browser).
20.open another windows powershell in administrator mode and type (minikube dashboard).
21.automatically opens.
22.kubectl delete deployment myngnix
23.minikube stop



nagios:
docker pull jasonrivers/nagios:latest
docker run -d --name nagiosdemo -p 8888:80 jasonrivers/nagios:latest
docker ps
http://localhost:8888     (username: nagiosadmin, password: nagios)
docker logs nagiosdemo
docker stop nagiosdemo
docker rm nagiosdemo
docker images
docker rmi jasonrivers/nagios:latest

5.go to services,Hosts etc. now in Hosts (it shows localhost, click on localhost).





AWS:
DEPLOYMENT of index.html using EC2 instance.
login to aws student login
dashboard->modules->launch AWS learner Academy lab->start lab(click on green aws lab->click EC2->launch instance3. ->Instance page is opened-->
4. Give a name to an instance under names and tags(MyExampleWebServer).
5. Under Application and OS images select ubuntu OS-->go for free tier option.
6. select the architecture as 64-bit(x86).
7. Instance type: h/w resources that u need like cpu,memory-->select t2.micro in this.
8.Give KeyPair name and click on create key pair & Save the .pem file in folder AWS on desktop
9.HERE select https and http in network settings
10.Now click on Launch Instance option at the bottom right.(AWS creates an instance.)
11.click on the instances at the top (after green ) once it is created select that instance(click checkbox and click on connect).connect to instance (copy ssh – i command).
12.Copy the path of .pem file (in power shell admin mode: cd <path of .pem file>.
13.paste the ssh -i cmd in windows shell.(now in ubuntu).
14.sudo apt update,sudo apt-get install docker.io,sudo apt install git,sudo apt install nano.
15.Create basic index.html file in folder Example in vscode.Open git Bash in folder Example by right clicking with mouse.
git init
git add .
git commit –m “first commit”
16.Create git repository (AWS).
git branch –M main
git remote add origin <https url of AWS repo>
git push –u origin main
refresh repository and You can now see index.html in github.Copy http path in code.
git clone <copied http url> in ubuntu in windows powershell.,ls,cd AWS,again ls(then index.html).
17.nano Dockerfile
inside it FROM nginx:alpine
           COPY . /usr/share/nginx/html (ctrl+s,ctrl+x)
18.in windows powershell-->sudo docker build –t mywebapp .
19.sudo docker run –d –p 80:80 mywebapp.
20.Go to instances and click on instance here i-0388... and then Copy public ipv4 address.
21.Paste it in the browser to get below output(which is in index.html).
22.sudo docker ps,sudo docker stop <container-id of mywebapp>.
23.Go back to instances.click on instance state and terminate instance. and end lab.





2 MAVEN WEB PROJECT DEPLOYMENT IN AWS:
1.click on start lab-->and then on aws-->click on EC2-->launch instance-->give name.(same OS t2.micro,free tier and all.
2.Create new key,Check all the boxes under network(http and https) and click  on launch instance at the bottom right.)
3.Click on instances,Wait until you get 2 tests passes,Click on connect after checking the box.
4.Copy ssh command,Open the terminal, Navigate to the path same like above (12 and 13 steps).
5.Run the ssh command.
6.sudo apt update,sudo apt-get install docker.io,sudo apt install git,sudo apt install nano.
7.Open MAVEN WEB PROJECT REPO in github and copy http link,Clone the repository,
8.If your repository is in main run following-->ls,cd MavenWebproject/.
9.in ubuntu itself: nano Dockerfile :  FROM tomcat:9-jdk11
                                        COPY target/*.war /usr/local/tomcat/webapps
10.sudo docker build –t mavenweb .
11.sudo docker run –d –p 9090:8080 mavenweb
12.Copy public ipv4: enter url in browser 54.87.134.240:9090/MavenWebproject.
13.If your app is not running goto security  and Click on security groups,Click on edit inbound rules,Click on add rule give port as 9090 and 0.0.0.0/0 click on save rules.
14.And refresh the page to check whether the web page has loaded or not.(success).
15.sudo docker ps,sudo docker stop <container-id of mavenweb>,next terminate instance and end lab.




Jenkins:
Maven Java :
 Step 1: Open Jenkins (localhost:8080)
   	 ├── Click on "New Item" (left side menu
Step 2: Create Freestyle Project (e.g., MavenJava_Build)
        	├── Enter project name (e.g., MavenJava_Build)
        	├── Click "OK"
└── Configure the project:
            		├── Description: "Java Build demo"
            		├── Source Code Management:
            			└── Git repository URL: [GitMavenJava repo URL]
            		├── Branches to build: */Main   or  */master
  		└── Build Steps:
               	     ├── Add Build Step -> "Invoke top-level Maven targets"
                  		└── Maven version: MAVEN_HOME
                 		└── Goals: clean
                	├── Add Build Step -> "Invoke top-level Maven targets"
                		└── Maven version: MAVEN_HOME
                		└── Goals: install
                	└── Post-build Actions:
                    	       ├── Add Post Build Action -> "Archive the artifacts"
                    			└── Files to archive: */
                    	     ├── Add Post Build Action -> "Build other projects"
                    			└── Projects to build: MavenJava_Test
                    			└── Trigger: Only if build is stable
                    	     └── Apply and Save


    └── Step 3: Create Freestyle Project (e.g., MavenJava_Test)
        	├── Enter project name (e.g., MavenJava_Test)
        	├── Click "OK"
              └── Configure the project:
             ├── Description: "Test demo"
             ├── Build Environment:
            		└── Check: "Delete the workspace before build starts"
            ├── Add Build Step -> "Copy artifacts from another project"
            		└── Project name: MavenJava_Build
            		└── Build: Stable build only  // tick at this
            		└── Artifacts to copy: */
            ├── Add Build Step -> "Invoke top-level Maven targets"
            		└── Maven version: MAVEN_HOME
            		└── Goals: test
            		└── Post-build Actions:
                ├── Add Post Build Action -> "Archive the artifacts"
                	└── Files to archive: */
                	└── Apply and Save

    └── Step 4: Create Pipeline View for Maven Java project
        ├── Click "+" beside "All" on the dashboard
        ├── Enter name: MavenJava_Pipeline
        ├── Select "Build pipeline view"         // tick here
         |--- create
        └── Pipeline Flow:
            ├── Layout: Based on upstream/downstream relationship
            ├── Initial job: MavenJava_Build
            └── Apply and Save OK

    └── Step 5: Run the Pipeline and Check Output
        ├── Click on the trigger to run the pipeline
        ├── click on the small black box to open the console to check if the build is success






Maven Web:
└── Step 1: Open Jenkins (localhost:8080)
    ├── Click on "New Item" (left side menu)
    
    └── Step 2: Create Freestyle Project (e.g., MavenWeb_Build)
        ├── Enter project name (e.g., MavenWeb_Build)
        ├── Click "OK"
        └── Configure the project:
            ├── Description: "Web Build demo"
            ├── Source Code Management:
            		└── Git repository URL: [GitMavenWeb repo URL]
            ├── Branches to build: */Main or master
            └── Build Steps:
                ├── Add Build Step -> "Invoke top-level Maven targets"
                	└── Maven version: MAVEN_HOME
                	 └── Goals: clean
                ├── Add Build Step -> "Invoke top-level Maven targets"
                	└── Maven version: MAVEN_HOME
                	└── Goals: install
                └── Post-build Actions:
                    ├── Add Post Build Action -> "Archive the artifacts"
                   	 └── Files to archive: */
                    ├── Add Post Build Action -> "Build other projects"
                    	└── Projects to build: MavenWeb_Test
                    	└── Trigger: Only if build is stable
                    └── Apply and Save

    └── Step 3: Create Freestyle Project (e.g., MavenWeb_Test)
        ├── Enter project name (e.g., MavenWeb_Test)
        ├── Click "OK"
        └── Configure the project:
            ├── Description: "Test demo"
            ├── Build Environment:
            		└── Check: "Delete the workspace before build starts"
            ├── Add Build Step -> "Copy artifacts from another project"
            		└── Project name: MavenWeb_Build
            		└── Build: Stable build only
            		└── Artifacts to copy: */
            ├── Add Build Step -> "Invoke top-level Maven targets"
           		└── Maven version: MAVEN_HOME
            		└── Goals: test
            └── Post-build Actions:
                ├── Add Post Build Action -> "Archive the artifacts"
                	└── Files to archive: */
                ├── Add Post Build Action -> "Build other projects"
                	└── Projects to build: MavenWeb_Deploy
                └── Apply and Save

    └── Step 4: Create Freestyle Project (e.g., MavenWeb_Deploy)
        ├── Enter project name (e.g., MavenWeb_Deploy)
        ├── Click "OK"
        └── Configure the project:
            ├── Description: "Web Code Deployment"
            ├── Build Environment:
            		└── Check: "Delete the workspace before build starts"
            ├── Add Build Step -> "Copy artifacts from another project"
            		└── Project name: MavenWeb_Test
            		└── Build: Stable build only
               	└── Artifacts to copy: */
            └── Post-build Actions:
                ├── Add Post Build Action -> "Deploy WAR/EAR to a container"
   └── WAR/EAR File: */.war or **/target/*.war target/myweb.war

   └── Context path: Webpath
 └── Add container -> Tomcat 9.x remote
└── Credentials: Username: admin, Password: 1234
── Tomcat URL: https://localhost:8085/
                └── Apply and Save

    └── Step 5: Create Pipeline View for MavenWeb
        ├── Click "+" beside "All" on the dashboard
        ├── Enter name: MavenWeb_Pipeline
        ├── Select "Build pipeline view"
        └── Pipeline Flow:
            ├── Layout: Based on upstream/downstream relationship
            ├── Initial job: MavenWeb_Build
            └── Apply and Save

    └── Step 6: Run the Pipeline and Check Output
        ├── Click on the trigger “RUN” to run the pipeline
Open Tomcat homepage in another tab
        ├── Click on the "/webpath" option under the manager app



Jenkins Build Triggers:
New item--> name--> select pipeline-->ok
description
Definition-->pipeline script-->
pipeline{
     agent any
     tools{
        maven 'MAVEN_HOME'
      }
     stages{
        stage('git repo & clean'){
             steps{
                 //bat "rmdir /s /q SampleMavenJavaProject"
                 bat "git clone https://github.com/Madhushalini921/SampleMavenJavaProject.git
                 bat "mvn clean -f SampleMavenJavaProject"
              }
          }
         stage('install'){
              steps{
                 bat "mvn install -f SampleMavenJavaProject"
              }
          }
         stage('test'){
               steps{
                   bat "mvn test -f SampleMavenJavaProject" (can also use mvn install -f SampleMavenJavaProject/pom.xml)
                }
          }
         stage('package'){
               steps{
                  bat "mvn package -f SampleMavenJavaProject"
                }
            }
        }
  }


apply and then save.
Build now.





Jenkins WebHooks:
1.https://ngrok.com :login with email.
2.go to nrok-amd64 path and click ngrok file(cmd prompt opens).
3.copy authtoken from ngrok
4.ngrok config add-authtoken <your_token>  in cmd.
5.ngrok http 8081 : type this in ngrok cmd .
6.Copy this URL only highlighted part : Forwarding lo upto dev 
7.Go to your GitHub repository,settings->webhooks-->add webhooks-->payload url(	Add url https://unhired-stormily-alaine.ngrok-free.dev/github-webhook/) like this.
8.Set content Type to application/json,just push event-->click on Add webhook to save
9.Open Jenkins Dashboard,Select the job (freestyle or pipeline) you’ve already created,Click Configure,Scroll down to the Build Triggers section,Check the box: GitHub hook trigger for GITScm polling.
10.Test the Setup
1.	Make any code update in your local repo and push it to GitHub.
2.	Once pushed, GitHub will trigger the webhook.
3.	Jenkins will automatically detect the change and start the build pipeline.
