# Deploy using simple yaml

We assume that you are in the folder that you have clone/fork the code.

1. Login to you cluster using the CLI
1. Create a new project.
    ```
    oc new-project manifest-demo
    ```
1. Apply the 3 yaml files
    ```
    oc apply -f manifest-demo/deployment.yaml
    ```
    ```
    oc apply -f manifest-demo/service.yaml
    ```
    ```
    oc apply -f manifest-demo/route.yaml
    ```

1. View the URL
    ```
    echo "$(oc  get route simple-quarkus-service --template='http://{{.spec.host}}')"
    ```

1. Retrieve the URL in a variable
    ```
    URL=$(oc  get route simple-quarkus-service --template='http://{{.spec.host}}')
    ```    
1. Take the url you have just retrieve with you favorite browser.

:tada: CONGRATULATIONS

You have now deploy the service using simple yaml files.

:point_right: Return: [Reposotory content](../README.md)