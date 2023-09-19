# Config Maps

**Existem duas fases na configuração de ConfMaps**
- 1ºcreate
- 2ºinject

Utilizámos confimaps para definirmos várias env variables to the pod

Commands:
- Kubectl get configmap
- Kubectl describe configmap 'name-configmap'


### Fase 1 (create configMap)

- Imperative:
```
        Kubectl create configmap
			<config-name> --from-literal=<key>=<value>
			
		Ex:
		Kubectl create configmap \
			App-config --from-literal=APP_COLOR=red
```

- Declarative:
```
	Kubectl create -f
	
	Config-map.yaml
		apiVersion: v1
		Kind: ConfigMap
		Metadata:
			Name: app-config
		Data:
			APP_COLOR: red
			APP_MODE: prod
```		
		
### ConfigMaps in PODS:
**NORMAL:**
```
Environment:
Spec:
	Containers:
		-name : my-app
		 image: nginx
		envFrom:
			- configMapRef: 
				name: app-config
```				


**SINGLES ENV:**
```
Spec:
	Containers:
		-name : my-app
		 image: nginx
		 env:
			-name: App_color
	         valueFrom:
		            configMapKeyRef:
					    Name: app-config
					    Key: APP_COLOR
```

**VOLUME:**
```
volumes:
	- name: app-config-volumes
	  configMap:
            Name: app-config
```