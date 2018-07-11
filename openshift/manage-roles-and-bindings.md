# Manage Roles and Bindings

### Create New Cluster Role

1. Export a cluster role as the template.

    ```sh
    oc get clusterrole system:hpa-patcher -o yaml > clusterrole.yaml
    ```

1. Edit the template for the new cluster role. For example:

    ```
    apiVersion: v1
    kind: ClusterRole
    metadata:
      name: custom:dc-patcher
    rules:
    - apiGroups:
      - ""
      attributeRestrictions: null
      resources:
      - deploymentconfigs
      verbs:
      - get
      - list
      - patch
      - watch
    ```

1. Create the new cluster role.

    ```sh
    oc create -f clusterrole.yaml
    ```

1. Add the new cluster role to an user.

    ```sh
    oadm policy add-cluster-role-to-user custom:dc-patcher <USERNAME>
    ```

1. Add the new cluster role to an user for *an specific project*.

    ```sh
    oadm policy add-role-to-user custom:dc-patcher <USERNAME> -n <PROJECT>
    ```

1. Verify the role-bindings.

    ```sh
    oc get rolebinding -n <PROJECT>
    oc describe clusterPolicyBindings :default
    ```

