- [Hollis](https://ibm.ent.box.com/folder/158173247216)
- [uncomment this line](https://github.com/hc-gitops-recipe-demo/multi-tenancy-gitops/blob/master/0-bootstrap/single-cluster/1-infra/kustomization.yaml#L23)
- [Templat.tf](https://github.com/IBM/cp4d-deployment/blob/master/common-modules/cpd/templates.tf)


<detalils>
    <summary>db2aaservice-cp4d-operator</summary>
    ### db2aaservice Cloud Pak for Data operator
    ```yaml
        #Db2aaservice
        data "template_file" "db2aaservice_sub" {
          template = <<EOF
        apiVersion: operators.coreos.com/v1alpha1
        kind: Subscription
        metadata:
          name: ibm-db2aaservice-cp4d-operator
          namespace: ${local.operator_namespace}
        spec:
          channel: ${var.db2_aaservice.channel}
          name: ibm-db2aaservice-cp4d-operator
          installPlanApproval: Automatic
          source: ibm-operator-catalog
          sourceNamespace: openshift-marketplace
        EOF
        }

        data "template_file" "db2aaservice_cr" {
          template = <<EOF
        apiVersion: databases.cpd.ibm.com/v1
        kind: Db2aaserviceService
        metadata:
          name: db2aaservice-cr
          namespace: ${var.cpd_namespace}
        spec:
          storageClass: ${local.storage_class}
          version: ${var.db2_aaservice.version}
          license:
            accept: true
            license: "Enterprise"
        EOF
        }
    ```

    </details>
