
# Kubernetes (K8s) - WordPress e MySQL
<img src="https://github.com/kubernetes/kubernetes/raw/master/logo/logo.png" alt="drawing" width="100"/> <img src="https://user-images.githubusercontent.com/112975441/202521730-762beeae-fc01-4711-9657-fab46c3c486e.png" width="100"> <img src="https://user-images.githubusercontent.com/112975441/202522596-0dcacd65-ffb6-49fd-b7c7-474d8b03c355.png" width="100">

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

# Usando o Minikube:
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

# Usando o Rancher no Linux:

- Abra o terminal do Ubuntu.

Digite: ```docker run -d --name rancher --restart=unless-stopped -v /opt/rancher:/var/lib/rancher  -p 80:80 -p 443:443 rancher/rancher:v2.4.3```

- Após, abra um navegador e digite :  ```localhost:80```.

- Feito isso estará dentro do Rancher.


# Usando o Minikube no Linux:

- Inicie o seu cluster com o minikube:

```
minikube start
```

- Habilitar o controlador Ingress:

```
minikube addons enable ingress
```

- Caso queira remover o cluster:

```
minikube delete
```

- Verifique se você já possui um cluster Kubernetes:

```
kubectl get nodes
```

# Realizar o Deploy do Wordpress

## Descrição dos arquivos:
 - 0-namespace.yaml: Cria um namespace chamado labwordpress, tudo o que for feito estará dentro deste namespace;
 - 1-pvc.yaml: Cria o recurso PersistentVolumeClaim para o servidor banco MysQL e Wordpress;
 - 2-mysql-deployment.yaml: Cria os recursos Secret, Service e Deployment para o banco MySQL;
 - 3-wordpress-deployment.yaml: Cria os recursos Service e Deployment para o Wordpress;
 - 4-ingress-wordpress.yaml: Criar o recurso Ingress para acessar o Wordpress através do domínio labwordpress.compass.com.
	
1. Aplique as configurações dos arquivos da pasta labwordpress:

```
kubectl apply -f labwordpress
```

2. Verifique se os Pods estão em execução:

```
kubectl get po --namespace labwordpress 
```

3. Listar namespaces:

```
kubectl get namespace --namespace labwordpress
```

4. Listar secrets:

```
kubectl get secret --namespace labwordpress
```

5. Listar pvc:

```
kubectl get pvc --namespace labwordpress 
```

6. Listar deployment:

```
kubectl get deployment --namespace labwordpress
```

7. Listar todos os recursos:

```
kubectl get all --namespace labwordpress
```

8. Excluir a aplicação:

```
kubectl delete -f labwordpress
```

9. Visualizar o estado do ingress da aplicação:

```
kubectl get ingress -n labwordpress
```

10. Visualizar o ingress da aplicação:

```
kubectl describe ingress -n labwordpress
```

11. Listar o serviço da aplicação:

```
kubectl get svc -n labwordpress
```

12. Descrever o serviço da aplicação:

```
kubectl describe svc -n labwordpress
```

13. Ver detalhes sobre o cluster:

```
minikube status
```

14. Os logs do Minikube podem ser acessados através do seguinte comando:

```
minikube logs
```

15. Acessar a aplicação Wordpress no cluster K8s
- No Browser de sua máquina, acesse o domínio e realize a instalação do Wordpress.

# Alterar o nome do domínio.

## Windows ##
- Navegar ao diretório: # cd C:\WINDOWS\system32\drivers\etc\
- Clicar no arquivo hosts.
- Executar o arquivo no Notepad++ como administrador.
- Atribuir uma nova linha no arquivo hosts contendo o IP do host e o nome do domínio.
- Ex: 127.0.0.1	labwordpress.compass.com

## Linux ##
- Entre no diretório raiz:
```
cd /
```	
- Conceda permissão de escrita para o arquivo hosts.

```
sudo chmod 777 /etc/hosts
```

- abra o arquivo hosts no editor.

```
vim /etc/hosts
```

>Obs: pressione a tecla i para entrar no modo de edição
	
- Edite o o arquivo hosts atribuindo uma nova linha com um ip padrão host(127.0.0.1) e logo após o nome do domínio:

Exemplo:

```
127.0.0.1	localhost
192.168.49.2    labwordpress.compass.com #linha acrescentada
```

>Obs: Para salvar basta pressionar ESC e digitar :wq! e dar enter.



- Depois de ter salvo as modificações do arquivo, volte a permissão padrão do arquivo:

```
sudo chmod 644 hosts
```

# Links para tentar solucionar alguns problemas que você possa vir a ter:
- https://kubernetes.io/pt-br/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
- https://github.com/kubernetes/minikube/issues/4172
- https://github.com/kubernetes/kubernetes/issues/50295
- https://discuss.kubernetes.io/t/the-connection-to-the-server-localhost-8080-was-refused-did-you-specify-the-right-host-or-port/1464/2
- https://github.com/Hawaiideveloper/Infastructure-as-Code-Sample_Env/issues/15#issuecomment-811377749
