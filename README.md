### Instalação do Ambiente

#### Java (JDK 17)

Para instalar o Java JDK 17, execute os seguintes comandos:

```bash
sudo apt update && sudo apt install openjdk-17-jdk -y
```

#### Jenkins

Para instalar o Jenkins, siga os passos abaixo:

1. Adicione a chave do Jenkins ao seu sistema:

    ```bash
    sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
      https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
    ```

2. Adicione o repositório do Jenkins à lista de fontes do apt:

    ```bash
    echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
    ```

3. Atualize a lista de pacotes e instale o Jenkins:

    ```bash
    sudo apt-get update && sudo apt-get install -y jenkins
    ```

#### Chave de Segurança

Para obter a senha inicial de administrador do Jenkins, execute o comando:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

#### Docker

Para instalar o Docker, siga os passos abaixo:

1. Adicione a chave GPG oficial do Docker:

    ```bash
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    ```

2. Adicione o repositório Docker às fontes do apt:

    ```bash
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```

3. Instale o Docker e seus componentes:

    ```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
    ```

4. Adicione o usuário atual e o usuário Jenkins ao grupo docker:

    ```bash
    sudo usermod -aG docker $USER
    sudo usermod -aG docker jenkins
    ```

5. Reinicie o Jenkins para aplicar as permissões no Docker:

    ```bash
    sudo systemctl restart jenkins
    ```

#### Kubectl

Para instalar o kubectl, siga os passos abaixo:

1. Adicione as chaves e repositórios necessários:

    ```bash
    sudo apt-get update
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg

    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    ```

2. Adicione o repositório do Kubernetes:

    ```bash
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
    sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list
    ```

3. Atualize a lista de pacotes e instale o kubectl:

    ```bash
    sudo apt-get update
    sudo apt-get install -y kubectl
    ```