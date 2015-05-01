JBoss BRMS Realtime Decision Server Demo 
========================================
This demo project will provide you with an example of creating, deploying and leveraging a set of rules
(decision table) in a Realtime Decision Server. You will be given examples of calling the rules as if
using it from an application with the RestAPI that is exposed.


Install on your machine
-----------------------
1. [Download and unzip.](https://github.com/jbossdemocentral/brms-coolstore-demo/archive/master.zip)

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

17. Query the Realtime Decision Server with loan rules by using POST method:

   - http://localhost:8080/kie-server/services/rest/server/containers/container-loan1.0

   - body of message can be found in support/loan-query.xml file, copy into Body section of RESTClient.


Notes
-----
You will need some sort of Rest client, such as the RESTClient Firefox extension which is used in this demo (screenshots and
videos). After installing RESTClient in Firefox, restart and open it under TOOLS menu.


Supporting Articles
-------------------
None yet..


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.0 JBoss BRMS 6.1 with demo rule project to deploy as Realtime Decision Server


