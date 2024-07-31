# Utilizing this organization

You'll need to check out all of these packages, remove all the IDs in the `sfdx-project.json` file.  Then you'll need to build the packages in a specific order.  Once the parent package is built and promoted, you'll need to copy the package ID (starts with `0Ho`) and the appropriate version ID (starts with `04t`) in the subsequent child package's `sfdx-project.json`

# Package order
* fflib-apex-mocks
* fflib-apex-common
* force-di
* at4dx
* core
* service
* service-escalations
* service-cs
* api
* api-service

# Create the package for the first time
```bash
NAME="namegoeshere"
sf org create scratch --alias scratch-$NAME -f config/project-scratch-def.json
sf project deploy start -o scratch-$NAME
sf package create --name $NAME --package-type Unlocked --path force-app
sf package version create --code-coverage --installation-key-bypass \
     --package $NAME --wait 5
sf package version promote --package $NAME@1.0.0-1
```
