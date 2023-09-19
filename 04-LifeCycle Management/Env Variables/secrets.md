# Secrets

### NOTE ON SECRETS

1. (negative) - Secrets are not Encrypted. Only enconded.
- (negative) - Do not check-in Secret objects to SCM along with code

2. (negative) -Secrets are not encrypted in ETCD
- (positive) - Enable encryption at rest
	
3. (negative) -Anyone able to create pods/deployments in the same namespace can access the secrets
- (positive) - Configure least-privilege access to Secrets - RBAC

4. (positive) -Consider third-party secrets store providers AWS, Azure, GCP, Vault


**Existem duas fases na configuração de Secrets**
- 1ºcreate
- 2ºinject


Commands:
- Kubectl get secrets
- Kubectl describe secrets 'name-secret'

### Fase 1 (create  Secrets)

- Imperative:
´´´
		Kubectl create secret generic
			<secret-name> --from-literal=<key>=<value>
			
		Ex:
		Kubectl create secret generic \
			App-secret --from-literal=DB_Host=mysql
´´´

- Declarative:
´´´
	Kubectl create -f
	
	Secret-data.yaml
		apiVersion: v1
		Kind: Secret
		Metadata:
			Name: app-secret
		Data:
			DB_Host: mysql
			DB_User: root
            ´´´

		
### Secrets in PODS:
**SECRETS in PODS:**
´´´	
Environment:
Spec:
	Containers:
		-name : my-app
		 image: nginx
		envFrom:
			- secretRef: 
				name: app-secret
´´´				
				
**SINGLES ENV:**
´´´	
Spec:
	Containers:
		-name : my-app
		 image: nginx
		 env:
			-name: App_sec
	            alueFrom:
		            secretKeyRef:
					    Name: app-secret
					    Key: DB_Host
´´´	


**VOLUME:**
´´´
volumes:
	- name: app-secret-volumes
	  secret:
		Name: app-secret
´´´		



ENCODE secrets

Echo -n 'mysql' | base64

DECODE secrets

Echo -n 'BKFWKN=l' | base64 --decode