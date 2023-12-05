# Changelog

## V1.1.6 - 17/11/2023

**SDK version :** 0.31.2 \
**API version :** 2023-11-13

- Fixed bugs and improvements

## V1.1.5 - 08/11/2023

**SDK version :** 0.31.1 \
**API version :** 2023-11-05

- Search bar added to projects page
- Added size limit for json entries in run_pipeline() SDK documentation
- Fixed bugs and improvements

## V1.1.4 - 02/11/2023

**SDK version :** 0.31.0 \
**API version :** 2023-10-30

- Compare execution for list metrics
- Add created_by , last_execution_id and deployments parameters to the return from get_pipeline()
- Deployment and pipeline slider -> display will evolve again
- Fixed bugs and improvements

## V1.1.3 - 24/10/2023

**SDK version :** 0.30.0 \
**API version :** 2023-10-23-2

- Added information to the return of get_deployment()
- Added the ability to add a description to a deployment
- Update information bubble infra env + associated tooltips
- Correction of filter overflows on small tables in the front end
- Fixed bugs and improvements

## V1.1.2 - 19/10/2023

**SDK version :** 0.29.0 \
**API version :** 2023-10-16-2

- Change of the output format of the size parameter of the functions get_data_store_object_information and list_data_store_objects.
    We now have str with the storage size units for a better readability of the file sizes.
- Fixed bugs and improvements

## V1.1.1 - 13/10/2023

**SDK version :** 0.28.0 \
**API version :** 2023-10-11

- Correction of blue screen in execution tracking when changing environment
- Requirement.txt path displayed in execution tracking
- Addition of get_user() function in SDK
- Added documentation on the maximum size of included_folders
- Fixed bugs and improvements

## V1.1.0 - 11/10/2023

**SDK version :** 0.27.1 \
**API version :** 2023-10-03

- GPU envs are available
- Step creation is limited to 3min max (the timeout_s parameter can be modified if necessary)
- Addition of pipeline duration in the experiment tracking
- Front-end correction (date in UTC and change GitHub references to Git)
- Fixed bugs and improvements


## V1.0.28 - 03/10/2023

**SDK version :** 0.27.0 \
**API version :** 2023-09-25

- Download button added to the execution comparison page
- Add inputs and outputs to the comparison execution page
- Wait for the step status to be ready before returning the result of create_step()
- Maximum size of code imported into a step increased from 1 MB to 5 MB
- Addition of a size limit for value-type I/O (JSON) 
- Fixed bugs and improvements

## V1.0.27 - 27/09/2023

**SDK version :** 0.25.0 \
**API version :** 2023-09-14

- Removal of the experimental mention on the tech doc for metrics and periodic deployment
- Fixed bugs and improvements

## V1.0.26 - 14/09/2023

**SDK version :** 0.24.1 \
**API version :** 2023-09-14

- Removal of the experimental mention on the tech doc for metrics and periodic deployment
- Fixed bugs and improvements

## V1.0.25 - 10/09/2023

**SDK version :** 0.24.0 \
**API version :** 2023-09-06

- I/O files can be downloaded from the Execution Tracking page
- Simple metrics can be viewed on the Execution Comparison page
- You can select the columns you want to display and filter/sort the metadata and simple metrics on the Execution Comparison page
- The repo, branch and Git commit can be viewed from the Execution Tracking page
- A limit of 100 simple metrics and 25 list metrics per step has been introduced
- We now use the d3 lib to display graphs
- It is now possible to have environments with GPUs (standard or medium)
- Added the Monitoring page (which lets you track pipeline metrics over a period)
- Added the delete_pipeline_execution(execution_id) function, which can be used to delete an execution using its execution_id

## V1.0.24 - 29/08/2023

**SDK version :** 0.23.2 \
**API version :** 2023-08-29

- Front improvement
- Bug fixes and improvements

## V1.0.24 - 29/08/2023

**SDK version :** 0.23.2 \
**API version :** 2023-08-29

- Front improvement
- Bug fixes and improvements

## V1.0.23 - 09/08/2023

**SDK version :** 0.23.1 \
**API version :** 2023-08-01

- Front improvement
- Bug fixes and improvements

## V1.0.22 - 01/08/2023

**SDK version :** 0.23.1 \
**API version :** 2023-08-01

- Front improvement (ISO format for dates)
- Bug fixes and improvements

## V1.0.21 - 26/07/2023


**SDK version :** 0.23.0 \
**API version :** 2023-07-26

- V1 run comparison page added
- Copy icon for the access path to the datastore in the front end
- Added parameter with created_by for the output of the list_pipeline_executions function in the SDK
- Bug fixes and improvements

## V1.0.20 - 18/07/2023

**SDK version :** 0.22.0 \
**API version :** 2023-07-18

- Possibility to delete a pipeline from front
- Bug fixes and improvements

## V1.0.19 - 06/07/2023

**SDK version :** 0.21.1 \
**API version :** 2023-07-06

- Dynamic path for outputs to datastore
- Some fixes on the list metrics front
- Internal usage metrics for list metrics added
- Bug fixes and improvements

## V1.0.18 - 28/06/2023

**SDK version :** 0.21.0 \
**API version :** 2023-06-28

- Front-end graphics for list metrics
- Commit id and branch name available in get_step and list_step
- Enhanced SDK doc with
    - Additional usage examples
    - More details on function returns
    - Flags for experimental features
- Bug fixes and improvements

## V1.0.17 - 20/06/2023

**SDK version :** 0.20.0 \
**API version :** 2023-06-2

- List metrics (without list metrics values in the frontend, only via SDK for now)
- Bug fixes and improvements

## V1.0.16 - 15/06/2023


**SDK version :** 0.19.0 \
**API version :** 2023-06-14

- Output mapping for run 
- Allow other repository than GitHub to fetch step code (example : GitLab) 
- Bug fixes and improvements

## V1.0.15 - 07/06/2023

**SDK version :** 0.18.0 \
**API version :** 2023-06-07

- Periodic deployment
- Datastore as source and destination for I/O files
- Fix for long runs with run_pipeline()
- Bug fixes and improvements

## V1.0.14 - 26/05/2023

**SDK version :** 0.17.0 \
**API version :** 2023-05-26

- Metrics pipeline (only for metrics with 1 value)
- Pipeline page in front
- Bug fixes and improvements

## V1.0.13 - 24/05/2023

**SDK version :** 0.16.0 \
**API version :** 2023-05-24

- Custom mappings for the execution pipeline are now available
- Ability to place env variables in the requirement path when creating a step
- Bug fixes and improvements

## V1.0.12 - 10/05/2023

**SDK version :** 0.15.0 \
**API version :** 2023-05-04

- Usage metrics (For internal use at Craft AI only)
- run_pipeline without custom mapping 
- Bug fixes and improvements

## V1.0.11 - 04/05/2023

**SDK version :** 0.15.0 \
**API version :** 2023-05-04

- Bug fixes and improvements

## V1.0.10 - 26/04/2023

**SDK version :** 0.14.1 \
**API version :** 2023-04-26

- Bug fixes and improvements

## V1.0.9 - 21/04/2023

**SDK version :** 0.14.0 \
**API version :** 2023-04-20

- Bug fixes and improvements

## V1.0.8 - 11/04/2023

**SDK version :** 0.13.2 \
**API version :** 2023-04-22

- Add environment page in the UI 
- Bug fixes and improvements

## V1.0.7 - 28/03/2023

**SDK version :** 0.13.1 \
**API version :** 2023-03-22

- Bug fixes and improvements

## V1.0.6 - 23/03/2023

**SDK version :** 0.13.0 \
**API version :** 2023-03-22

- Add error messages on the build of steps
- Added object STEP_PARAMETER to explain step creation parameters between "fall back on project info" and "null"
- Added function get_data_store_object_information()
- is_null source is now available for all input type
- Fix endpoint mapping with is_required parameter (which was mandatory)
- Various fixes and improvements

## V1.0.5 - 15/03/2023


**SDK version :** 0.13.0 \
**API version :** 2023-03-15

- New front page for input/output in execution tracking
- Add ability to create a step with a custom dockerfile
- Add function list_pipelines() to get list of all pipelines
- Bug fixes

## V1.0.4 - 28/02/2023

**SDK version :** 0.12.0 \
**API version :** 2023-02-24

- Added ability to trigger endpoint with file input/output in io feature
- Fixed input mapping 'isRequired' matches step input
- Fixed issue with refreshing environments and deployments lists in the frontend
- Fixed default value for included folders

## V1.0.3 - 17/02/2023

**SDK version :** 0.11.0 \
**API version :** 2023-02-17

- Fix input mapping bug with constant source
- Add Google Tag Manager
- Rework login page
- Other bug fixes

## V1.0.2 - 15/02/2023

**SDK version :** 0.10.1 \
**API version :** 2023-02-13

- Rename force_step_deletion to force_dependents_deletion
- Bug fix

## V1.0.1 - 10/02/2023

**SDK version :** 0.10.0 \
**API version :** 2023-02-06

- Project information from GitHub is taken into account for step creation (and therefore optional at this stage)
- Improve error messages for step creation
- Message for first login
- Front improvement/correction
- Bug correction

## V1.0.0 - 27/01/2023

**SDK version :** 0.9.0 \
**API version :** 2023-01-26

- Adds separate environments for each project.
- Input/output (IO) added to steps. 
- Added IO mapping for the endpoint
- Add automatic redirection to wait for pipeline output.
- Syntax change: force_endpoints_deletion replaced by force_deployments_deletion.
- When executions are retrieved, two variables are added to the result:
    - start_date for the ;
    - end_date for pipelines and stages.
