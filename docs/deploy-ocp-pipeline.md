# Deploy Using OpenShift Pipeline

We assume that you are in the folder that you have clone/fork the code. For instructions on how to install OpenShift Pipiline you can refer to my [OpenShift Pipeline Demo](https://github.com/froberge/ocp-pipeline-demo) in this [section](https://github.com/froberge/ocp-pipeline-demo/blob/main/docs/install-pipeline-operator.md)

1. Login to you cluster using the CLI
1. Make sure you are in the pipeline-demo folder
`.../pipeline-demo/`
1. Using `Kustomize` create the different resources needed to run the demo
    ```
    oc apply -k .
    ```
    Result:
    ```
    namespace/pipeline-demo created
    service/simple-quarkus-service created
    deployment.apps/simple-quarkus-service created
    route.route.openshift.io/simple-quarkus-service created
    pipeline.tekton.dev/simple-quarkus-service created
    eventlistener.triggers.tekton.dev/github-webhook created
    triggerbinding.triggers.tekton.dev/github-pr-trigger-binding created
    triggertemplate.triggers.tekton.dev/simple-quarkus-service-trigger-template created
    persistentvolumeclaim/maven-repo-pvc created
    persistentvolumeclaim/sources-pvc created
    ```
1. Let's expose the trigger service
    ```
    oc expose svc el-github-webhook -n pipeline-demo
    ```
    ```
    oc get route el-github-webhook -n pipeline-demo
    ```
1. Retrive the trigger url.
    ```
    echo "$(oc  get route el-github-webhook -n pipeline-demo  --template='http://{{.spec.host}}')"
    ```
1.  Create the GitHub Webhook

    Open [GitHub](https://github.com/)  in the right repository, go to setting -> Webhook -> Add Webhook

    _Before you click Add webhook it should look similar to this. With the URL retrieve step 5._

    ![Webhook](/docs/images/github-webhook.png)

    You can now push a change to the repository, it should trigger the pipeline.
    
1. Open OpenShift console and validate the the pipeline is running.


:tada: CONGRATULATIONS

You have now deploy the service using OpenShift Pipeline.

:point_right: Return: [Reposotory content](../README.md)