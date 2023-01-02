# Pré-requisitos

## Seleção do Recipe

Adicione o caminho do _singularity recipe_ desejado na variável RECIPE no github (projeto >> Settings >> Secrets >> New Secret).

# Template Integração Contínua Github

Esse projeto o template para uso do cluster da UFSCar, contendo integração contínua com o Google Drive e Amazon S3.

## Requisitos para Google Drive

1. Entre no [console de credenciais de API do Google](https://console.developers.google.com/apis/credentials)
2. Se ainda não houver um projeto, crie um.
3. Em "Ativar API e Serviços", busque por "Google Drive" e ative a permissão.
4. Clique em "Criar credenciais".
5. Selecione "ID do cliente do OAuth".
6. Em "Tipo de aplicativo", selecione "App para computador".
7. Dê um nome de identificação para as credenciais e clique em "criar". Vão aparecer dois dados ("Seu ID de cliente" e "Sua chave secreta de cliente"), precisaremos dos dois no passo seguinte.
8. Acesse o _cluster_, execute o comando `rclone config` e forneça as seguintes informações quando solicitado:

```
n/s/q> n
name> cloud
Storage> 17 # selecione aqui o número correspondente a opção "Google Drive"
client_id> conteúdo de "Seu ID de cliente"
client_secret> conteúdo de "Sua chave secreta de cliente"
scope> 1  # Full access all files, excluding Application Data Folder
root_folder_id> deixe em branco
service_account_file> deixe em branco
y/n> deixe em branco
y/n> n

Se já tiver o rclone instalado em seu computador, execute o comando exibido, caso contrário, o instale conforme indicado na página oficial do rclone dependendo do seu sistema operacional (https://rclone.org/install/). A Seguir insira o resultado do comando exibido:

config_token> código fornecido pelo terminal após autorização
y/n> deixe em branco
y/e/d> deixe em branco
e/n/d/r/c/s/q> q
```

A configuração até agora servirá para transferência de dados do _cluster_ para a nuvem e vice-e-versa. A partir de agora vamos configurar a integração contínua no github.

8. Execute o comando:

```
echo $(cat ~/.config/rclone/rclone.conf | base64 --wrap=0)
```

9. Copie a saída e adicione à variável RCLONE_CONF no github.
10. Adicione no github à variável COLLECTION_CONTAINER `/path/to/project`, esse será o caminho cujo container vai ser disponibilizado no seu Google Drive no formato `recipe_name_DateTime.simg`.

## Requisitos para Amazon S3

1. Entre na [AWS](console.aws.amazon.com)
2. Clique na seta ao lado de seu nome de usuário e em "My Security Credentials".
3. Na seção "Access Keys", clique em "Create New Access Key".
4. Na janela que aparece, clique em "Show Access Key".
5. Acesse o _cluster_, execute o comando `rclone config` e forneça as seguintes informações quando solicitado:

```
n/s/q> n
name> cloud
Storage> 4
provider> 1
env_auth> 1
access_key_id> conteúdo de "Access Key ID"
secret_access_key> conteúdo de "Secret Access Key"
region> 16
endpoint> deixe em branco
location_constraint> 16
acl> deixe em branco
server_side_encryption> deixe em branco
sse_kms_key_id> deixe em branco
storage_class> deixe em branco
y/n> deixe em branco
y/e/d> deixe em branco
e/n/d/r/c/s/q> q
```

A configuração até agora servirá para transferência de dados do _cluster_ para a nuvem e vice-e-versa. A partir de agora vamos configurar a integração contínua no github.

6. Execute o comando:

```
echo $(cat ~/.config/rclone/rclone.conf | base64 --wrap=0)
```

7. Copie a saída e adicione à variável RCLONE_CONF no github.
8. Adicione no github à variável COLLECTION_CONTAINER `/path/to/project`, esse será o caminho cujo container vai ser disponibilizado no seu Google Drive no formato `recipe_name_DateTime.simg`
