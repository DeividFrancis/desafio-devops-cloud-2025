## Comandos que eu usei que vi na aula e meu entendimento de cada coisa

- AWS: Criar usuarios (boas praticas e segurança)
### Criar roles (IAM)
  - eks-cluster
    - AmazonEKSClusterPolicy
  - eks-worker
    - AmazonEC2ContainerRegistryReadOnly
    - AmazonEKSWorkerNodePolicy
    - AmazonEKS_CNI_Policy

### Criar rede (CloudFormation)

- [Template padrao AWS para EKS](https://s3.us-west-2.amazonaws.com/amazon-eks/cloudformation/2020-10-29/amazon-eks-vpc-private-subnets.yaml)

- Usa opção de URL cola esse link
- Defina apenas o nome o resto deixa padrão
- Demora mesmo... (pramin deu 3m)
- Depois de esta Up verifica la em VPC (tem que ter <NOME_QUE_VC_COLOCO>-VPC)

### Criar cluster kubernetes (EKS)

#### Step 01
- Não usa eks auto mode (Vi em outros videos que você deixa de aprender quando a aws cuida demais do seu cluster)

- coloca a role `eks-cluster`
- usei a versão `1.31` (porque era a mais atual)

#### Step 02
- Não usa a VPC padrão mas sim a que você criou antes
- Coloca todas as sub-redes
- `Additional security groups - optional` - Coloca a `ControlPlaneSecurityGroup` que criou junto com a vpc 
- Deixa Public and private

#### Step 04
- "Modo vida loka", como e teste não precisa habilitar metricas e etc

#### Step 05
- Deixa os Add-ons padrão mesmo

#### Step 06
- Deixa como está

#### Step 07
- É so revisão então é só criar e ser filix :)
- Demora mesmo... (pramin foi 6m)

### Usar o eks na minha maquina

- Instalar o `awscli` em https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
- Tudo certo `aws --version`
- Precisa logar na aws, vai no `IAM/Users/<MEU-USUARIO>/Security credentials/Access keys/Create access key`
  - Escolhe a opção `Command Line Interface (CLI)`
- Volta no terminal e roda `aws configure` e cola as credenciais 
- Puxar as configs do cluster `aws eks update-kubeconfig --name <EKS-NAME>`

### Configura perfil das maquinas do meu cluster

- Na aws vai em para criar as ec2 `EKS/Clusters/<EKS-NAME>/Node groups/Add node group`
- Pode ter varios como 'aplicações, sistemas'

#### Step 01
- Coloca o nome e a role `eks-worker`

#### Step 02
- Deixa padrão pois e teste mesmo
- Isso tambem vai ser cobradro (tanto gerencia o EKS e criar maquinas EC2)

#### Step 03
- Quais sub-redes os nodes vão se comunicar
- Boa pratica deixa somente nos nodes `PRIVATE`, remove os publicos
- Demora mesmo... (pramin foi 2m)
- No terminal e para aparecer alguma coisa quando roda `kubectl get nodes` 

### Deploy

#### Docker build/push
`docker build -t deividoliver/fake-shop:v1 --push .`
#### Manifesto postgres
#### Manifesto fake-shop

- `kubectl rollout restart deployment <nome-do-deployment>` usei para força o pull da imagem com a mesm tag

### Apagar tudo apra não ter custo

- CLI: Deletar deploy `kubectl delete -f k8s/deployment.yaml`
- AWS: Deletar `EKS/Clusters/aula-eks/Node groups/default`
- Demora mesmo... (+- 8m)
- AWS: Deletar `EKS/Clusters/aula-eks`
- Demora mesmo... (+- 3m)
- AWS: Deletar network `CloudFormation/Stacks`
- Demora mesmo... (+- 3m)

