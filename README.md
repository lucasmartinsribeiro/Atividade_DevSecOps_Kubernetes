# Atividade_DevSecOps_Kubernetes
Repositório destinado ao versionamento da atividade de Kubernetes do PB DevSecOps da Compass.uol.

# Instalação do Docker Desktop no Windows
  - Utilize a documentação disponibilizada no site do Docker: https://docs.docker.com/desktop/install/windows-install/

# Instalação Docker Engine para Ubuntu Usando Repositório

1. Desinstale versões mais antigas do Docker.

```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

2. Atualize os pacotes do computador.

```
sudo apt-get update
```
3. Instale os pacotes para permitir o acesso ao repositório HTTPS.

```
sudo apt-get install \
 ca-certificates \
 curl \
 gnupg \
 lsb-release
```

4. Adicione a chave GPG oficial do Docker.

```
sudo mkdir -p /etc/apt/keyrings
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
5. Configura o repositório.

```
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

6. Atualize os pacotes novamente.
	
```
sudo apt-get update
```
>Em caso de erro na atualização dos pacotes tente definir o umask do computador com o comando:

```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

7. Instale a versão mais recente do Docker Engine.

```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

8. Instalar Rancher - Single Node

```
docker run -d --name rancher --restart=unless-stopped -v /opt/rancher:/var/lib/rancher  -p 80:80 -p 443:443 rancher/rancher:v2.4.3
```

9. Inicie o seu cluster com o minikube

```
minikube start
```

10. Executar os arquivos
```
kubectl create -f nome-de-cada-arquivo
```

12. Criar um url para ter acesso a aplicaçao
```
minikube service wordpress --url
```
