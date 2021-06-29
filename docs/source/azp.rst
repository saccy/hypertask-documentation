Azure Pipelines
===============

Azure Pipelines are offered as products to your customers.

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
               "choices_list": [
                  "Hello",
                  "Bonjour",
                  "G'day"
               ]
         },
         "string_example": {
               "friendly_name": "Input example",
               "meta": "Who are you greeting? This is an example of a string input.",
               "default": "World!"
         }
      },
      "artifacts": {
         "Test artifact": "artifact.txt"
      },
      "supplemental_pipelines": {
         "Supplement example": {
               "def_id": 8,
               "desc": "Runs a pipeline that downloads the artifact from the original build and cats the content."
         }
      }
   }
