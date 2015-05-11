JBoss BRMS Loan Realtime Decision Server Demo 
=============================================
This demo project will provide you with an example of creating, deploying and leveraging a set of rules
(decision table) in a Realtime Decision Server. You will be given examples of calling the rules as if
using it from an application with the RestAPI that is exposed.

There are two options for you to install this project; local and containerized.


Option 1 - Install on your machine
----------------------------------
1. [Download and unzip.](https://github.com/jbossdemocentral/brms-loan-realtime-decicion-server-demo/archive/master.zip)

2. Add products to installs directory.

3. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges.

4. Start JBoss BRMS Server by running ./target/jboss-eap-6.4/bin/standalone.sh

5. Login to http://localhost:8080/business-central

    ```
    - login for admin and analyst roles (u:erics / p:jbossbrms1!)
    ```
6. Project has simple data model (Loan & Applicant) and single decision table credit score rule set.

7. Build and deploy version 1.0 of project.

8. View Authoring -> Artifact repository to see deployed loandemo-1.0.jar artifact.

9. Open rule deployments perspective via menu Deploy -> Rules Deployments

10. Register a new server by filling in pop-up:

  - Endpoint: http://localhost:8080/kie-server/services/rest/server/
  
  - Name: DevServer (...as we are testing this in our dev environment)

  - Username: erics (...who must have role of kie-server)

  - Password: jbossbrms1!

11. Provision starts by creating a Container, click on DevServer '+' on right.

  - Name: container-loan1.0

  - search button gathers all artifacts available, SELECT loandemo-1.0 to auto-fill rest of fields

  - click on OK

12. Container is created, click on icon far right to view details.

13. Select container-loan1.0 and click START to get it up and running, was orange color next to name, should turn green.

14. See 'Resolved Release Id' section for the container and version that is running and ready for rule queries.

15. Using Firefox + RESTClient you can see which server containers are available by:

   - Add auth credentials in menu Authentication - Basic Authentication:  Username: erics    Password: jbossbrms1!

   - Method: GET

   - URL: http://localhost:8080/kie-server/services/rest/server/containers

   - it will show container = contianer-loan1.0, meaning our container is available via the provided RestAPI 

16. You can view some more information provided by the RestAPI using GET methods:

   - http://localhost:8080/kie-server/services/rest/server/containers/container-loan1.0

17. Now to use POST or PUT methods we need to add a header to RESTClient for our requests:

   - in menu Headers -> Custom Header

   - Name: Content-Type

   - Value: application/xml

18. Query the Realtime Decision Server with loan rules by using POST method:

   - http://localhost:8080/kie-server/services/rest/server/containers/container-loan1.0

   - body of message can be found in support/loan-query.xml file, copy into Body section of RESTClient.

   - note you can adjust the credit score field in the xml message body to show rows in decision table being used.

19. You can change the decision table as desired, redeploy a new version, use the Server Management Browser to manage the container
		using UPGRADE button to pull the latest version.

   - you need to deploy a new version of the rules, for example version 1.1, then enter 1.1 in version field of container-loan1.0
     before hitting UPGRADE button.

20. For creation or deletion of containers in the RestAPI, you need to use PUT methods, see product documentation User Guide for
		details.


Option 2 - Generate containerized install
-----------------------------------------
The following steps can be used to configure and run the demo in a container

1. [Download and unzip.](https://github.com/jbossdemocentral/brms-realtime-decicion-server-demo/archive/master.zip)

2. Add product installer to installs directory.

3. Copy contents of support/docker directory to the project root.

4. Build demo image.

	```
	docker build -t jbossdemocentral/brms-realtime-decicion-server-demo .
	```
5. Start demo container.

	```
	docker run -it -p 8080:8080 -p 9990:9990 jbossdemocentral/brms-realtime-decicion-server-demo
	```
6. Follow instructions from above starting at step 5 replacing *localhost* with *&lt;RH_CONTAINER_HOST&gt;* when applicable

Additional information can be found in the jbossdemocentral container [developer repository](https://github.com/jbossdemocentral/docker-developer)


Notes
-----
You will need some sort of Rest client, such as the RESTClient Firefox extension which is used in this demo (screenshots and
videos). After installing RESTClient in Firefox, restart and open it under TOOLS menu.


Supporting Articles
-------------------
[Getting Started with the Realtime Decision Server](http://www.schabell.org/2015/05/jboss-bpmsuite-quick-guide-getting-started-realtime-decision-server.html)


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.1 JBoss BRMS 6.1 with demo rule project to deploy as Realtime Decision Server and Red Hat Container install option.

- v1.0 JBoss BRMS 6.1 with demo rule project to deploy as Realtime Decision Server


![Digital Sign](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/digital-sign.jpg)

![Loan Project](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/loan-prj-overview.png)

![Artifact Repo](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/artifact-repo-loandemo.png)

![Deployment View](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/clean-rules-deployment-view.png)

![Kie Server Endpoint](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/kie-server-endpoint.png)

![Register Server](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/register-dev-server.png)

![Dev Server](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/dev-server.png)

![Create Container](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/create-container.png)

![Container Details](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/container-details.png)

![Start Container](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/start-container.png)

![Started Container](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/started-container.png)

![Restapi Auth](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/restapi-basic-authentication.png)

![Restapi Containers](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/restapi-containers.png)

![Restapi Loan Container](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/restapi-container-loan1.0.png)

![Restapi Request Header](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/restapi-request-header.png)

![Restapi Loan Request](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/restapi-loan-request.png)

![Restapi Loan Request Response](https://raw.githubusercontent.com/jbossdemocentral/brms-loan-realtime-decision-server-demo/master/docs/demo-images/restapi-loan-request-response.png)

