# Importing Custom Applications in HPE Ezmeral Unified Analytics

Describes how to import, manage, and secure applications and frameworks in HPE Ezmeral Unified Analytics Software. Imported and included applications appear in the Applications & Frameworks screen in HPE Ezmeral Unified Analytics Software.

This repo will go over the steps required to import custom Kubernetes Applications. 

### Importing Custom Kubernetes Application

Detail instructions can be found [here](https://support.hpe.com/hpesc/public/docDisplay?docId=a00eaf10hen_us&page=ManageClusters/managing-application-lifecycle.html)


### Import Applications

 ####  Step 1: Enter Framework details
![import_new_app_screen_#1](https://github.com/ranjitreddy2013/UnifiedAnalyticsImportApps/assets/5430682/786c0d48-9920-446a-bbe2-8f45d666d668)

#### Step 2: Enter Framework chart details
![hello_world_chart_value](https://github.com/ranjitreddy2013/UnifiedAnalyticsImportApps/assets/5430682/98c244f5-f3df-4b70-8b16-17e89155a552)

#### Step 3: Review Framework values in yaml
![hello_world_review_framework_values](https://github.com/ranjitreddy2013/UnifiedAnalyticsImportApps/assets/5430682/cf9fa007-f044-453e-8660-87c0ab153079)

#### Step 4: Review Framework Summary
![hello_world_review_values](https://github.com/ranjitreddy2013/UnifiedAnalyticsImportApps/assets/5430682/54c7b851-593f-433f-945e-23b30fa491a8)

#### Step 5: Monitor new Framework status : Installing
![hello_world_installing](https://github.com/ranjitreddy2013/UnifiedAnalyticsImportApps/assets/5430682/baadbcbf-6561-497c-8032-79c235c1a4e1)

#### Step 6: Monitor new Framework status : Ready
![hello_world_installed](https://github.com/ranjitreddy2013/UnifiedAnalyticsImportApps/assets/5430682/7d2648bc-afb1-4c85-b38b-91f39489d5da)

#### Troubleshooting tips
If there is a failed attempt of the new Framework. You might see a message "Framework file exists.". To fix this error, you  have to delete it from [ChartMuseum](https://chartmuseum.com/docs/). 
To access ChartMuseum API, you first  need to expose the service endpoint. Here are the steps:
1) Login to k8s workload cluster master node or use the KubeConfig to access the API
2) Expose the service/chartmuseum, as shown below. When the service is exposed command does not return, but the port on the node is forwarded to the pod.
```
[root@mip-mapr-prod05 ~]# kubectl port-forward service/chartmuseum -n ez-chartmuseuns 8082:8080
Forwarding from 127.0.0.1:8082 -> 8080
Forwarding from [::1]:8082 -> 8080
```
Once the service is exposed, you can delete the imported framework from command line, in the below command, "hello-world" is the name of the framework, 0.1.0 is the version.
```
[root@mip-mapr-prod05 ~]# curl -X DELETE http://localhost:8082/api/charts/hello-world/0.1.0
{"deleted":true}
[root@mip-mapr-prod05 ~]#
```
