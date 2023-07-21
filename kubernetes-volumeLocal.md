## Crie um StorageClass
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: registry-sc
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
```

## Crie a pasta do Volume no servidor desejado
```
mkdir -p /disks/registry-volume
chmode 777 /disks/registry-volume
```

## Crie o PersistentVolume e especifique o servidor
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: registry-pv
spec:
  storageClassName: registry-sc
  persistentVolumeReclaimPolicy: Retain
  capacity:
    storage: 70Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  local:
    path: /disks/registry-volume
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - server-04
```

## Crie o PersistentVolumeClaim
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: registry-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: registry-sc
  resources:
    requests:
      storage: 60Gi
```

## Crie o POD que irá utilizar o Volume
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: registry-deploy
spec:
  template:
    metadata:
      name: registry-pod
      labels:
        server: registry-pod
    spec:
      containers:
        - name: registry-app
          image: universointeligente/registry-local:0.3
          ports:
            - containerPort: 5000
          volumeMounts:
            - name: volume-registry
              mountPath: "/var/lib/registry"
        - name: registry-ui
          image: joxit/docker-registry-ui:latest
          ports:
            - containerPort: 80
      volumes:
        - name: volume-registry
          persistentVolumeClaim:
            claimName: registry-pvc
      imagePullSecrets:
        - name: regcred
  replicas: 1
  selector:
    matchLabels:
      server: registry-pod
```
