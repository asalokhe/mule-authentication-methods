# mule-connected-app
  Application demonstrating various authentication methods for mule app deployments.
  Check various branches for different methods. 
-   Deployment of mule application to cloudhub using username and password

    **Branch Name: username-password**

-   Deployment of mule application to cloudhub using connected app

    **Branch Name: connected-app**

-   Deployment of mule application to cloudhub using username and password from Settings.xml

    **Branch Name: username-password-ext-setting**


## Prerequisite:
1. Create a User or Connected app with required scope.

   Note that the connected App credentials must have the **Design Center Developer** access scope.
   
   ![Connected-App](Images/Connected-App.png)
2. Mule Applicaiton


## Deployment of mule application to cloudhub using username and password

```sh
    <configuration>
        <cloudHubDeployment>
            <uri>https://anypoint.mulesoft.com</uri>
            <muleVersion>${app.runtime}</muleVersion>
            <username>${username}</username>
            <password>${password}</password>
            <applicationName>${cloudhub.application.name}</applicationName>
            <environment>${environment}</environment>
            <objectStoreV2>true</objectStoreV2>
            <properties>
            <key>value</key>
            </properties>
        </cloudHubDeployment>
    </configuration>
```

```sh
    mvn clean package deploy -DmuleDeploy 
        -Dapp.runtime=<<Runtime-Version>> \
        -Dusername="<username>" \
        -Dpassword="<password>" \
        -Dcloudhub.application.name="<<Unique-app-Name>>" \
        -Denvironment=<<Environment>>
```

## Deployment of mule application to cloudhub using connected app

```sh
    <configuration>
        <cloudHubDeployment>
            <uri>https://anypoint.mulesoft.com</uri>
            <muleVersion>${app.runtime}</muleVersion>
            <connectedAppClientId>${client.id}</connectedAppClientId>
            <connectedAppClientSecret>${client.secret}</connectedAppClientSecret>
            <connectedAppGrantType>${grant.type}</connectedAppGrantType>
            <environment>${environment}</environment>
            <objectStoreV2>true</objectStoreV2>
            <properties>
            <key>value</key>
            </properties>
        </cloudHubDeployment>
	</configuration>
```

```sh
    mvn clean package deploy -DmuleDeploy 
        -Dapp.runtime=<<Runtime-Version>> \
        -Dclient.id="<connected-app-client-id>" \
        -Dclient.secret="<connected-app-client-secret>" \
        -Dgrant.type="client_credentials" \
        -Dcloudhub.application.name="<<Unique-app-Name>>" \
        -Denvironment=<<Environment>>
```

## Deployment of mule application to cloudhub using username and password from Settings.xml

pom.xml
```sh
    <configuration>
        <cloudHubDeployment>
            <uri>https://anypoint.mulesoft.com</uri>
            <muleVersion>${app.runtime}</muleVersion>
            <server>my.server.cred.id</server>
            <applicationName>${cloudhub.application.name}</applicationName>
            <environment>${environment}</environment>
            <objectStoreV2>true</objectStoreV2>
            <properties>
            <key>value</key>
            </properties>
        </cloudHubDeployment>
    </configuration>
```

settings.xml
```sh
    <server>
        <id>my.server.cred.id</id>
        <username>USERNAME</username>
        <password>PASSWORD</password>
    </server>
```

```sh
    mvn clean package deploy -DmuleDeploy 
        -Dapp.runtime=<<Runtime-Version>> \
        -Dcloudhub.application.name="<<Unique-app-Name>>" \
        -Denvironment=<<Environment>>
```
## References:
-   https://docs.mulesoft.com/access-management/connected-apps-overview
-   https://help.mulesoft.com/s/article/How-to-use-Connected-Apps-with-CI-CD
-   https://docs.mulesoft.com/exchange/to-publish-assets-maven#publish-and-consume-federated-assets
-   https://docs.mulesoft.com/mule-runtime/4.4/deploy-to-cloudhub

