# sidecar

# Uruchomienie poda  
`kubectl apply -f sidecar-pod.yaml`  

# Przekierowanie portu nginx  
`kubectl port-forward sidecar-pod 8080:80`  
![Alt text](Screenshot 2023-10-22 113243.png)

# Sprawdzenie zawartości udostępnianej przez nginx
```
$req = curl -Uri http://localhost:8080/date.log
$req.rawContent

![Alt text](Screenshot 2023-10-22 113137.png)
```
