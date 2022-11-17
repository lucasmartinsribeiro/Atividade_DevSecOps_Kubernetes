
# Kubernetes (K8s)
<img src="https://github.com/kubernetes/kubernetes/raw/master/logo/logo.png" alt="drawing" width="100"/>
Esse repositório tem como objetivo mostrar como subir uma aplicação Wordpress + DB Mysql utilizando kubernetes.

# Requisitos necessários para execução dessa atividade:

-  Instalar o docker desktop. https://docs.docker.com/desktop/install/windows-install/
-  Instalar o kubectl.
-  Instalar o minikube. 
-  Verificar Wsl e o Hiper-V.

# Usando o Rancher:

- Abra o terminal do Ubuntu ou o powershell se estiver usando o Windows.

Digite: ```docker run -d --name rancher --restart=unless-stopped -v /opt/rancher:/var/lib/rancher  -p 80:80 -p 443:443 rancher/rancher:v2.4.3```

- Após, abra um navegador e digite :  ```localhost:80```.

- Feito isso estará dentro do Rancher.

# O que você precisará para instalar o minikube:
- 2 CPUs ou mais
- 2 GB de memória livre
- 20 GB de espaço livre em disco
- conexão de internet
- Gerenciador de contêiner ou máquina virtual, como: Docker , Hyperkit , Hyper-V , KVM , Parallels , Podman , VirtualBox ou VMware Fusion/Workstation

- No linux ubuntu: 

- Vá até o terminal e digite : ``` curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube ```

- Logo após digite : ``` minikube start ```
- Com o minikube instalado prossiga digitando : ```kubectl get po -A```
- O minikube pode baixar a versão apropriada do kubectl e você poderá usá-lo assim:```minikube kubectl -- get po -A```
- Para obter informações adicionais sobre o estado do cluster, o minikube inclui o Kubernetes Dashboard, permitindo que você se adapte facilmente ao seu novo ambiente:
- ```minikube dashboard ```

- No powershell do Windows:

  - ```New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri  'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing```
  
  - Adicione o minikube.exebinário ao seu arquivo PATH.
  
 ``` $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine) if ($oldPath.Split(';') -inotcontains 'C:\minikube'){ `
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine) `} ```
  
 - Daí é só repetir o mesmo processo feito nos passos de Linux.

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

11. Criar um url para ter acesso a aplicação
```
minikube service wordpress --url
```
