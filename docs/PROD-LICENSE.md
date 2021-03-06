# Ping Identity DevOps - Obtaining Product License

In order to run the Ping Identity DevOps images, a valid product license is
required.  There are several ways to obtain a product license
to run the images:

* Eval License - By providing your Ping Identity DevOps User and Key
  * Obtaining a Ping Identity DevOps User and Key
  * Saving your DevOps User/Key
  * Using your DevOps User/Key
* Existing license - By embedding into your Server Profile
  * Obtaining an evaluation license via your Ping Identity Account Profile
  * Use an existing license file (Current customers)


## Obtaining a Ping Identity DevOps User and Key
Ping Identity will provide a DevOps Key to any user registered as a 
developer with Ping Identity.
You must follow the steps listed below to obtain a Ping Identity DevOps User and Key

* Ensure you are enrolled in the Ping Identity Developer Program.  Not sure, click the link for [Join developer program](https://www.pingidentity.com/en/account/register.html?type=developer) and follow instructions.
  * If you don't have an account, please create one.
  * Otherwise, sign-in.
  * Your DEVOPS-USER is your email.
  ![images/PROD_LICENSE_1.png](images/PROD_LICENSE_1.png)
* Request your DEVOPS-KEY from the [FORM](https://docs.google.com/forms/d/e/1FAIpQLSdgEFvqQQNwlsxlT6SaraeDMBoKFjkJVCyMvGPVPKcrzT3yHA/viewform).

You should now have a DEVOPS-USER and DEVOPS-KEY.

Example:
* `PING_IDENTITY_DEVOPS_USER=jsmith@example.com`
* `PING_IDENTITY_DEVOPS_KEY=e9bd26ac-17e9-4133-a981-d7a7509314b2`

## Saving your DevOps User/Key
The best way to save your DevOps User/Key is to use the Ping Identity Config command ``piconfig``.  You can run this
if you have setup your environment using the ``setup`` command that comes with the ``pingidentity-devops-getting-started``
github repo.  More details on this can be found in that [quickstart](getting-started/QUICKSTART.md).

Simpy run:

```
piconfig
```

and answer the propmpt with your DEVOPS User/Key.  You can view these settings with the ``denv`` command after you've
configured them.

## Using your DevOps User/Key
When starting an image, you can provide your devops property file ``~/.pingidentity/devops`` or using
the individual environment variables.  For more detail, run the ``denv`` to get your devops environment
information.  

### Example with docker run command
An example of running a docker image using the
`docker run` command would look like the following
example (See the 2 environment variables starting with **PING_IDENTITY_DEVOPS**):

```
docker run \
           --name pingdirectory \
           --publish 1389:389 \
           --publish 8443:443 \
           --detach \
           --env SERVER_PROFILE_URL=https://github.com/pingidentity/pingidentity-server-profiles.git \
           --env SERVER_PROFILE_PATH=getting-started/pingdirectory \
           --env-file ~/.pingidentity/devops \
           pingidentity/pingdirectory
```

### Example with .yaml file
An example of running a docker image using any docker .yaml file
would look like the following example (See the 2 environment variables 
starting with **PING_IDENTITY_DEVOPS**):

```
...
  pingdirectory:
    image: pingidentity/pingdirectory
    env_file:
      - ${HOME}/.pingidentity/devops
    environment:
      - SERVER_PROFILE_URL=https://github.com/pingidentity/pingidentity-server-profiles.git
      - SERVER_PROFILE_PATH=getting-started/pingdirectory
...
``` 

## Using an existing Product License file
You can also use an existing valid product licsen file the the product/version combo
you are running, by placing them into the proper directory of your server profile.
The default server profile location and file name for each product are as follows:

Note: You do not need to do this if you are using your DevOps User/Key.  If you have
provided license files as part of your server profile and a DevOps User/Key, it will
ignore the DevOps User/Key.

* PingFederate - `instance/server/default/conf/pingfederate.lic`
* PingAccess - `instance/conf/pingaccess.lic`
* PingDirectory - `instance/PingDirectory.lic`
* PingDataSync - `instance/PingDirectory.lic`

## Troubleshooting
If you have any quesitons or issues, please contact [devops_program@pingidentity.com](mailto:devops_program@pingidentity.com).
