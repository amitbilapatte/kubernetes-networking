# kubernetes-networking

- To connect pods with each other we have **three different options**

    + look up for IP address and manually enter it in value:

        env:
            - name: AUTH_ADDRESS
            value: "10.103.152.86"
            <!-- this IP is available on auth-service after running "kubectl get services" after deploying "kubectl apply -f=auth-service.yml -f=auth-deployment.yml" -->
    + or use kubernetes feature which provides this automatically generated env variables as address in follow:

        - in kubenetes, we can dynamically fetch this value by :
        `${process.env.AUTH_SERVICE_SERVICE_HOST}` 
        - syntax is `AUTH_SERVICE_SERVICE_HOST` : `auth-service` (service name in Capital and dash("-") is replaced by underscore("_") ) + then `_SERVICE_HOST`.

    + or use aitomatically generated domain names : 
        domain names are genearated for every service launched in cluster, we can use that domain name from inside cluster to send request there
        env:
          - name: AUTH_ADDRESS
            value: "auth-service.default" 
    <!-- servicename.namespacename (if we don't define namespace it is "default") -->
