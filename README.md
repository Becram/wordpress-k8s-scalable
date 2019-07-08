# wordpress-k8s-scalable

# 1. Setup MySQL Secrets

> *Quickstart option:* In this repository, run `bash scripts/quickstart.sh`.

Create a new file called `password.txt` in the same directory and put your desired MySQL password inside `password.txt` (Could be any string with ASCII characters).


We need to make sure `password.txt` does not have any trailing newline. Use the following command to remove possible newlines.

```bash
tr -d '\n' <password.txt >.strippedpassword.txt && mv .strippedpassword.txt password.txt
```

# 2. Create Local Persistent Volumes
To save your data beyond the lifecycle of a Kubernetes pod, you will want to create persistent volumes for your MySQL and Wordpress applications to attach to.


# Troubleshooting

If you accidentally created a password with newlines and you can not authorize your MySQL service, you can delete your current secret using

```bash
kubectl delete secret mysql-pass
```

If you want to delete your services, deployments, and persistent volume claim, you can run
```bash
kubectl delete deployment,service,pvc -l app=wordpress
```

If you want to delete your persistent volume, you can run the following commands
```bash
kubectl delete -f local-volumes.yaml
```

If WordPress is taking a long time, you can debug it by inspecting the logs
```bash
kubectl get pods # Get the name of the wordpress pod
kubectl logs [wordpress pod name]
```
