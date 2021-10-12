# CICD

In this blog we will try to learn how we can install TeamCity Server and Agent as docker image and required configuration.

# What is TeamCity?

TeamCity is a build management and continuous integration server from JetBrains.

CI/CD Pipeline

# Features of TeamCity
It provides several ways to reuse the settings of the parent project to subproject.
For a single build Teamcity can take source code from two different VCS.
It can also detect builds which are hung.
For easy access you can mark build.
We can run parallel builds simultaneously in different environments.
Formatted text can be set for Build status which makes the server perform some actions.
You can build docker images in separate steps with the extension to other runners (Gradle, Maven, etc).
Testers can be replaced with agents.

# Download and Install TeamCity:
In this blog I am going to show how you can install dockerised versions of TeamCity Server and Agent.
Download TeamCity Server Image using below command
docker pull jetbrains/teamcity-server
For more info refer here.
Download TeamCity Server Image using below command
docker pull jetbrains/teamcity-agent
For more info refer here.

# Run TeamCity Server:
Use Below command to run TeamCity Server
docker run -d — name teamcity-server-instance -v /opt/docker/teamCity/teamcity_server/datadir:/data/teamcity_server/datadir -v /opt/docker/teamCity/teamcity_server/logs:/opt/teamcity/logs -p 9111:8111 jetbrains/teamcity-server
Check status using below command
docker ps

Docker Process Status

# Configure TeamCity Server:
Open http://<Server-IP>:<Port>

TeamCity Setup
Click On Proceed

TeamCity Setup — Database Type Selection
Click On Proceed, Wait as it will take some time to configure.

Team City Setup — Tems & Conditions
Check “Accept license agreement” and Click on “Continue”

TeamCIty Setup — Admin Account Setup
Provide required detail and click on “Create Account”
Note: As I am going to use TeamCity for Demo so configuring it default setting.

# Run TeamCity Client:
Use Below command to run TeamCity Agent
docker run -d — name teamcity-agent-instance -e SERVER_URL=”http://teamcity-server-instance:8111" — link teamcity-server-instance -v /opt/docker/teamCity/teamcity_agent/conf:/data/teamcity_agent/conf jetbrains/teamcity-agent
Check status using below command
docker ps

Docker Process Status

# Configure TeamCity Agent:
Run TeamCity Agent (using above command if using dockrised version)
Open to TeamCity Server URL in browser
http://192.168.56.101:9111/login.html

TeamCity Login Page
Provide required information and click on “Log In”

TeamCity Home Page
Click on Agent Tab

TeamCity Agents Tab
Now you can see Unauthorized (1) means you are agent is running successfully
Click on Unauthorized Tab

TeamCity Unauthorized Agents
You can see one Agent is showing as Connected, Click on Authorize

TeamCity Agent Registration
Provide a comment and Click on Authorize
Agent will appear in Connected Tab now

TeamCity Connected Agents
Done.
Now we are ready to use TeamCity.

# Advantages of TeamCity:
Server and Agent are platform independent and can install anywhere
Automated Deployment
Integration using any SCM tools.
Check History and Status of Build JOBS.
# Disadvantages of TeamCity:
Upgrading from one version to another causes a lot of work to be done.
Teamcity is not open source after 3 agents and 100 builds users need to take license and to be paid.
The user community for TeamCity is very less as compared to other CI tools in the market.
