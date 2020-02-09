# Using Persistent Volume on StatefulSets with no-provisioner StorageClass

A set of definitions for using PVs on StatefulSets

## Gotchas

1. PersistentVolumeReclaimPolicy

	Given that you are using a no-provisioner StorageClass, means that your PV is not dynamically provisioned. It means that you are left with one choice and that is `Retain`

	Once you have bounded to a PV, don't delete the PVC pointing to it. Otherwise you would be in a world of hurt (if you dont have storage-admin or cluster-admin permissions) since you would be begging someone who has that permission to help you delete & recreate the PVs.

	Note: Recyle PersistentVolumeReclaimPolicy has been deprecated in favor of Dynamic Provisioning. See https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims

2. PersistentVolumeClaims

	Once you have your PV & StorageClass created, and StatefulSet definition ready, doing `oc create -f <statefuleset definition>` PVC will automatically be created

## Misc

1. pv0088.yml
	
	nodeAffinity value used was derived from the output of `oc get nodes`. 
