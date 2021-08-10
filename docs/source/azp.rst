Azure Pipelines
===============

Azure Pipelines are offered as products to your customers.

You can offer them in 3 ways:

* Free: No restriction, guest users can run.
* One-off purchases: Users must register/log in in order to purchase and run.
* Subscriptions: Users must register/log in in order to purchase and run.

In order to import an Azure DevOps account you need to be logged in as an `admin` user.

Navigate to the ``Integrations`` view, select Azure DevOps from the dropdown and then select ``Add Azure DevOps account``.
You will need to provide your Azure DevOps organization, project and PAT. The PAT provided needs to be able to run your pipelines and download pipeline artifacts.

Once you've added an ADO account you can start importing pipelines.

Currently, Hypertask only supports pipelines that use Azure Git as their pipeline source, i.e. you'll need to create an ADO git repo in the same project as your pipeline and use that as your source.
Addtionaly, only repo's that have a ``hypertask_params.json`` file in their root will be identified as available for importation.

The ``hypertask_params.json`` file for a free pipeline must be in this format::

   {
      "name": "Hello, World!",
      "short_desc": "An example of a free product",
      "long_desc": "It might not look like much, but this task runs an Azure Pipeline in the background that produces an artifact based on your inputs. You can download the artifact right here on hypertask after the task completes by navigating to the 'Manage orders' section under the account drop-down. You can also run an associated pipeline from the same page.",
      "type": "free",
      "inventory_group": "Examples",
      "tags": [],
      "params": {
         "choices_example": {
               "friendly_name": "Choices example",
               "meta": "Choose a greeting. This is an example of a list of choices.",
               "unique": false,
               "choices_list": [
                  "Hello",
                  "Bonjour",
                  "G'day"
               ]
         },
         "string_example": {
               "friendly_name": "Input example",
               "meta": "Who are you greeting? This is an example of a string input.",
               "default": "World!",
               "unique": false
         }
      },
      "artifacts": {
         "Test artifact": "artifact.txt"
      },
      "supplemental_pipelines": {
         "Supplement example": {
               "def_id": 12,
               "desc": "Runs a pipeline that downloads the artifact from the original build and cats the content."
         }
      }
   }


The ``hypertask_params.json`` file for a one-off purchase pipeline must be in this format::

   {
      "name": "AWS web app stack",
      "short_desc": "An example of a one off purchase",
      "long_desc": "Here we are simulating the creation of a 'web app stack' wherein we deploy an EC2 instance and an RDS instance.",
      "type": "one-off",
      "inventory_group": "AWS",
      "tags": ["infrastructure"],
      "price": 5.99,
      "params": {
         "os": {
               "friendly_name": "Operating system",
               "meta": "Choose an operating system for your app to run on",
               "unique": false,
               "choices_list": [
                  "Windows Server 2019",
                  "CentOS 7"
               ]
         },
         "db": {
               "friendly_name": "Database",
               "meta": "Choose the RDS database type for your app to integrate with",
               "unique": false,
               "choices_list": [
                  "Microsoft SQL server 2019",
                  "PostgreSQL 13.2"
               ]
         }
      }
   }


The ``hypertask_params.json`` file for a subscription pipeline must be in this format::

   {
      "name": "VPN",
      "short_desc": "Deploys a secure, managed VPN server that you will have exclusive access to. No lock in, cancel at any time",
      "long_desc": "You will need to install the OpenVPN client on your local machine. Once the deployment is finished you will be issued an OpenVPN certificate. You need to add the certificate to the OpenVPN client on your machine in order to connect to your VPN server",
      "type": "subscription",
      "inventory_group": "Subscriptions",
      "tags": ["DigitalOcean"],
      "params": {
         "location": {
               "friendly_name": "Location",
               "meta": "Where do you want your VPN server to be located?",
               "unique": false,
               "choices_list": [
                  "Singapore",
                  "New York",
                  "Amsterdam",
                  "San Francisco",
                  "London",
                  "Frankfurt",
                  "Toronto",
                  "Bangalore"
               ]
         }
      },
      "artifacts": {
         "VPN certificate": "client.ovpn"
      },
      "supplemental_pipelines": {
         "Unsubscribe": {
               "def_id": 2,
               "desc": "Cancels your subscription and deletes your VPN server."
         }
      }
   }
