# Accessing Tanzu Application Platform GUI

Use one or two methods to access Tanzu Application Platform GUI:

* Use the default LoadBalancer method
* Use a shared Ingress method


## <a id="lb-method"></a> LoadBalancer Method

Verify that you specified the `service_type` for Tanzu Application Platform GUI in your
Tanzu Application Platform values YAML file as in this example:

```
tap_gui:
  service_type: LoadBalancer
```

Follow these steps:

1. Obtain the external IP of your LoadBalancer by running:

    ```
    kubectl get svc -n tap-gui
    ```

1. Access Tanzu Application Platform GUI by using the external IP with the default port of 7000.
It has the following form:

    ```
    http://EXTERNAL-IP:7000
    ```


## <a id="ingress-method"></a> Ingress Method

The `Ingress` method of access for Tanzu Application GUI can use the shared `tanzu-system-ingress`
instance of Contour that is installed as part of the Profile installation.

1. For the `Ingress` method of access to work, you need a DNS host name that you can point at the External IP address of the `envoy` service that the shared `tanzu-system-ingress` uses. Retrieve this IP address by running:

    ```
    kubectl get service envoy -n tanzu-system-ingress
    ```

    This returns a value similar to this example:

    ```
    kubectl get service envoy -n tanzu-system-ingress
    NAME    TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
    envoy   LoadBalancer   10.0.242.171   40.118.168.232   80:31389/TCP,443:31780/TCP   27h
    ```

    The IP address in the `EXTERNAL-IP` field is the one that you point a DNS host record at.
    Tanzu Application Platform GUI automatically prepends `tap-gui` to your provided subdomain.
    This makes the final host name `tap-gui.example.com`. You use this host name in the appropriate
    fields in the `tap-values.yml` mentioned later.

1. Specify parameters in your `tap-values.yaml` related to Ingress as in this example:

    ```
    tap_gui:
      service_type: ClusterIP
      ingressEnabled: "true"
      ingressDomain: 'example.com' # This makes the host name tap-gui.example.com
    ```

1. Update your other host names in the `tap_gui` section of your `tap-values.yml` with the new host name as in this example:

    ```
    tap_gui:
      service_type: ClusterIP
      ingressEnabled: "true"
      ingressDomain: 'example.com' # This makes the host name tap-gui.example.com
        # Existing tap-values.yml above  
        app_config:
        app:
            baseUrl: http://tap-gui.example.com # No port needed with Ingress
        integrations:
            github: # Other are integrations available
            - host: github.com
                token: GITHUB-TOKEN
        catalog:
            locations:
            - type: url
                target: https://GIT-CATALOG-URL/catalog-info.yaml
        backend:
            baseUrl: http://tap-gui.example.com # No port needed with Ingress
            cors:
                origin: http://tap-gui.example.com # No port needed with Ingress
    ```

    This snippet is from a values file in the
    [Configure Tanzu Application Platform GUI section](../install.md#configure-tap-gui) of the
    Profiles installation topic. The new host names are populated based on the example host name
    `tap-gui.example.com`.

1. Update your package installation with your changed values file by running:

    ```
    tanzu package installed update tap --package-name tap.tanzu.vmware.com --version 0.4.0 --values-file TAP-VALUES-FILE.yml -n tap-install
    ```

    Where `TAP-VALUES-FILE` is the name of your Tanzu Application Platform values YAML file.

1. Access your Tanzu Application Platform GUI by using a web browser at the host name you provided.