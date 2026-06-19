### Task 1: Create a ConfigMap from Literals
1. Use `kubectl create configmap` with `--from-literal` to create a ConfigMap called `app-config` with keys `APP_ENV=production`, `APP_DEBUG=false`, and `APP_PORT=8080`
2. Inspect it with `kubectl describe configmap app-config` and `kubectl get configmap app-config -o yaml`
3. Notice the data is stored as plain text — no encoding, no encryption
   
<img width="1687" height="707" alt="image" src="https://github.com/user-attachments/assets/d2ef7520-fd84-4f2b-bcc9-0e329b6a650f" />

**Verify:** Can you see all three key-value pairs?
* yes
---

### Task 2: Create a ConfigMap from a File
1. Write a custom Nginx config file that adds a `/health` endpoint returning "healthy"
2. Create a ConfigMap from this file using `kubectl create configmap nginx-config --from-file=default.conf=<your-file>`
3. The key name (`default.conf`) becomes the filename when mounted into a Pod
**Verify:** Does `kubectl get configmap nginx-config -o yaml` show the file contents?

<img width="1342" height="572" alt="image" src="https://github.com/user-attachments/assets/59d28d06-4011-4924-be0b-2ec3f2c89896" />

-------


### Task 3: Use ConfigMaps in a Pod
1. Write a Pod manifest that uses `envFrom` with `configMapRef` to inject all keys from `app-config` as environment variables. Use a busybox container that prints the values.

2. Write a second Pod manifest that mounts `nginx-config` as a volume at `/etc/nginx/conf.d`. Use the nginx image.

4. Test that the mounted config works: `kubectl exec <pod> -- curl -s http://localhost/health`

Use environment variables for simple key-value settings. Use volume mounts for full config files.

<img width="1085" height="983" alt="image" src="https://github.com/user-attachments/assets/7a2093ee-926d-47f3-9a82-e2c82ceedbdd" />

**Verify:** Does the `/health` endpoint respond?
* yes

------

### Task 5: Use Secrets in a Pod
1. Write a Pod manifest that injects `DB_USER` as an environment variable using `secretKeyRef`
2. In the same Pod, mount the entire `db-credentials` Secret as a volume at `/etc/db-credentials` with `readOnly: true`
3. Verify: each Secret key becomes a file, and the content is the decoded plaintext value

<img width="1020" height="830" alt="image" src="https://github.com/user-attachments/assets/24afc633-00d2-44fb-88a1-efe09c918a61" />

**Verify:** Are the mounted file values plaintext or base64?
* in plaintext .
------

### Task 6: Update a ConfigMap and Observe Propagation
1. Create a ConfigMap `live-config` with a key `message=hello`
2. Write a Pod that mounts this ConfigMap as a volume and reads the file in a loop every 5 seconds
3. Update the ConfigMap: `kubectl patch configmap live-config --type merge -p '{"data":{"message":"world"}}'`
4. Wait 30-60 seconds — the volume-mounted value updates automatically
5. Environment variables from earlier tasks do NOT update — they are set at pod startup only

<img width="812" height="998" alt="image" src="https://github.com/user-attachments/assets/8e3769b3-87f6-46c3-baee-7550eb213db0" />
<img width="1242" height="115" alt="image" src="https://github.com/user-attachments/assets/63c82d15-53d8-452c-ae0c-87ee48b348da" />

**Verify:** Did the volume-mounted value change without a pod restart?
* no
-----------

### Task 7: Clean Up
Delete all pods, ConfigMaps, and Secrets you created.

<img width="787" height="525" alt="image" src="https://github.com/user-attachments/assets/007565ef-80e3-4303-a398-b31344a37c8a" />

-----
