# update-infra-deployments

* This task clones a GitHub repository specified in the 'targetGHRepo' key of the input data file.
* If 'targetGHRepo' is not provided, it defaults to 'defaultTargetGHRepo: redhat-appstudio/infra-deployments'.
* It then runs a script obtained from the 'infra-deployment-update-script' key in the data file, which can modify text files.
* Finally, it generates a pull request for the specified repository using the modified files.


## Parameters
| Name                    | Description                                                                                  | Optional | Default Value                                                                                                                                    |
|-------------------------|----------------------------------------------------------------------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| dataJsonPath            | Path to data json file. It should contain a key called 'infra-deployment-update-script'      | false    |                                                                                                                                                  |
| snapshotPath            | Path to snapshot json file                                                                   | false    |                                                                                                                                                  |
| originRepo              | URL of github repository which was built by the Pipeline                                     | false    |                                                                                                                                                  |
| revision                | Git reference which was built by the Pipeline                                                | false    |                                                                                                                                                  |
| defaultTargetGHRepo     | GitHub repository of the infra-deployments code                                              | true     | redhat-appstudio/infra-deployments                                                                                                               |
| gitImage                | Image reference containing the git command                                                   | true     | registry.redhat.io/openshift-pipelines/pipelines-git-init-rhel8:v1.8.2-8@sha256:a538c423e7a11aae6ae582a411fdb090936458075f99af4ce5add038bb6983e8 |
| scriptImage             | Image reference for SCRIPT execution                                                         | true     | quay.io/mkovarik/ose-cli-git:4.11                                                                                                                |
| sharedSecret            | Secret in the namespace which contains private key for the GitHub App                        | true     | infra-deployments-pr-creator                                                                                                                     |
| githubAppID             | ID of Github app used for updating PR                                                        | true     | 305606                                                                                                                                           |
| githubAppInstallationID | Installation ID of Github app in the organization                                            | true     | 35269675                                                                                                                                         |

## Changes in 1.0.0
- Modified `update-infra-deployments` task to dynamically fetch `targetGHRepo` from the `dataJsonPath` JSON file.
(defaults to 'redhat-appstudio/infra-deployments').
- Updated task description to reflect the dynamic repository selection.
- Added defaultTargetGHRepo parameter to the update-infra-deployments task to specify the
  default GitHub repository for infra-deployments.

## Changes since 0.4.1
- Updated hacbs-release/release-utils image to reference redhat-appstudio/release-service-utils image instead

## Changes since 0.4.0
- add protection to prevent failures if there are no updated files.

## Changes since 0.3
- extraDataJsonPath is renamed to dataJsonPath to more closely match the API spec

## Changes since 0.2
- update Tekton API to v1

## Changes since 0.1
- extraDataJsonPath and snapshotPath are now required parameters
