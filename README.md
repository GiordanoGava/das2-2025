### Design e Arquitetura de Software
Giordano Bruno Gava

### Aula 27/02/2025

Best Practices for building solutions on AWS

# -> Trade-offs
    (Fazer escolhas)

    + Por exemplo: escolher uma linguagem de programação.

    + Consistência, durabilidade, latência e tamanho são exemplos de características para o seu software. Mas todos custam bastante, então você deve fazer escolhas, 
    ...qual deles faz mais sentido para você, e em que momento essas características serão mais "usadas".
    + Para novas ferramentas, priorize velocidade de produção ao invés de custo.
    + Baseie decisões de desing em dados empíricos.

    + Terceira fórmula normal serve para reduzir redundâncias.

        (3FN) -> A terceira forma normal ( 3NF ) é uma abordagem de design de esquema de banco de dados para bancos de dados relacionais 
        que usa princípios de normalização para reduzir a duplicação de dados, evitar anomalias de dados , garantir integridade referencial 
        e simplificar o gerenciamento de dados.

    
# -> Implementando escalabilidade

    + Tenha certeza que a sua arquitetura consiga lidar com mudanças em demanda

    Melhor prática-> https://miro.medium.com/max/875/1*ejKvErfBZHWUqjTCj2w0DA.png

    1. O serviço nunca é interrompido para os usuários
    2. Servidores de aplicação no limite de alarme 
    3. O Amazon EC2 Auto Scaling é alertado e dimensionado
    4. O novo servidor fica pronto antes de atingir a capacidade


# -> Automatizando seu ambiente

    + Automatize o suprimento, a rescisão, e a configuração de recursos.

    1. Server da aplicação crasha
    2. Amazon CloudWatch avisa automaticamente a parte que crashou
    3. Amazon EC2 Escala sozinho, lança e configura um server identico
    4. Um alarme notifica o admin
    5. CloudWatch automaticamente log a ação para gerenciar uma solução


# -> Using IaC

    + Provisione a sua infraestrutura computacional usando código ao invés de processos manuais.


# -> AWS infraestructure topics 

    + AWS Regions
        -> É um local físico em todo o mundo onde agrupamos datacenters.
        -> Cada região da AWS consiste em várias AZs isoladas e separadas fisicamente em uma área geográfica.
    + Availability Zones
        -> Data center que possui sua própria infraestrutura de Hardware, Rede, Segurança e redundância de energia.
    + AWS Local Zones
        -> Basicamente uma "Regions" só que de tamanho menor.
    + AWS data centers
    + AWS points of presence (PoPs)
        -> Os PoPs são como portas de entrada para a nuvem da AWS, permitindo o roteamento de tráfego de maneira eficiente e a entrega de conteúdo com baixa latência.


# -> Securing Access, tópicos de segurança

    + IaaS/EC2 -> Infraestrutura como serviço -> Servidor
        -> AWS é responsável pelo servidor que a empresa estiver usando. No caso a parte física, de hardware.
        -> A parte digital é responsabilidade do cliente.
    + SaaS/PaaS/S3 -> Operation system, network e firewall é responsabilidade da AWS quando o assunto é o S3.
    + Provedor de indentidade forte
        -> Proteger dados em trânsito e repouso -> HTTPS
    + Aplicar segurança em todas as camadas
        -> Na maioria das empresas os únicos métodos de segurança são o firewall e o antivírus.
            -> Hoje em dia isso não é mais suficiente.
    + Manter os dados longe das pessoas
        -> Não dar acesso direto as fontes de dados.
    + Ter Rastreablididade.
    + Estar preparado para possíveis eventos de segurança.
        -> Ter uma equipe 24/7 procurando erros.
    + Automatizar as melhores práticas de segurança.


# -> Permissão de usuário para acessar os recursos

    + Autenticação
        -> O que eu sei (senha)
        -> O que eu sou (biometria)
        -> O que eu tenho (celular/pc/etc)

    + Permissão 
        -> Quem está logado, apenas deve acessar aquilo que deveria ver.

    + Princípio do privilégio mínimo
        -> Dar o mínimo de permissões possíveis para o usuário


# -> Recurso IAM

    + O AWS Identity and Access Management (IAM) é um serviço da Amazon Web Services (AWS) que permite controlar o acesso aos recursos da AWS.

    + Criação de contas IAM
        -> Se cria acesso programatico através da Access Key e Secret Key
        -> A conta tem que ter um tempo de duração
        -> Use senhas fortes e complexas
        -> Use senhas rotativas, de tempos em tempos troque a Access Key
        -> Guarde as credenciais de forma segura
        -> Acessos programáticos
            -> AWS Api Rest
            -> AWS SDK
            -> AWS CLI
    

# -> Como dar permissões à usuários.
        
    + Mecanismo de permissionamento (RBAC - Role Base Access Control) 
    + De acordo com meu papel (role), tenho certas permissões.


# -> Lab Policy : Permissões
            
    + Existem algumas roles pré prontas, gerenciadas pela AWS
        -> Identity-based
        -> Usuários IAM: São identidades individuais associadas a uma pessoa ou processo. Os usuários podem ser atribuídos a políticas que concedem permissões específicas para acessar os serviços e recursos da AWS.
        -> Grupos IAM: São coleções de usuários. As permissões são atribuídas a grupos, e qualquer usuário dentro do grupo herdará essas permissões.
        -> Roles IAM: São funções atribuídas a entidades (usuários, serviços da AWS, etc.) que exigem permissões específicas. Em um laboratório, você pode ter uma role com permissões limitadas apenas ao acesso de recursos necessários para o exercício.


# -> Resource-based
    
    + Políticas de Bucket S3: Permitem controlar quem pode acessar os arquivos no bucket.
    + Políticas de IAM Role: Podem ser usadas para permitir que um serviço acesse recursos específicos, como permitir que um EC2 tenha permissão para acessar um bucket S3.

    + Todo Bucket ao ser criado é privado, e deve-se tornar público.
        -> Amazon Resource Name (Identificador único)
        -> Permito que qualquer usuário possa listar objetos do meu bucket.


# -> Tipos de armazenamento

    + Block storage
    + File storage
        -> Estrutura hierarquica
    + Object storage
        -> Baseado em atributos de meta-data


# -> Policy de Identidade 

    + Controla o que usuários ou funções IAM podem fazer nos recursos da AWS.


# -> Policy de Recurso 
    
    + Controla quem pode acessar e fazer o quê em um recurso específico (ex: bucket S3).


# -> S3

    + Serviço de armazenamento de objetos da AWS, usado para guardar e recuperar dados na nuvem.

    + S3 - Ciclo de Vida:
        -> Automatiza a movimentação/exclusão de objetos S3, otimizando custos.
    + S3 - Versionamento:
        -> Guarda múltiplas versões de arquivos S3, para recuperação de dados.
    + S3 - CORS:
        -> Permite que sites acessem arquivos S3 de outros domínios.

        -> Isso é uma configuração de CORS:

            [
                {
                    "AllowedHeaders": [
                        "*"
                    ],
                    "AllowedMethods": [
                        "GET",
                        "PUT",
                        "POST",
                        "DELETE"
                    ],
                    "AllowedOrigins": [
                        "http://127.0.0.1:5500" 
                    ],
                    "ExposeHeaders": [
                        "x-amz-server-side-encryption",
                        "x-amz-request-id",
                        "x-amz-id-2"
                    ],
                    "MaxAgeSeconds": 3000
                }
            ]


# -> Diga de documentação do githubCP

    + https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/github-copilot-chat-cheat-sheet


# -> EC2 (Elastic Compute Cloud)

    + Serviço de computação que permite criar e gerenciar instâncias (servidores virtuais) na AWS, com flexibilidade para escolher o tipo de instância e escalabilidade de recursos conforme a demanda.


# -> EBS (Elastic Block Store)

    + Armazenamento persistente e de alto desempenho para dados, utilizado por instâncias EC2. É independente das instâncias e permite fácil backup e escalabilidade.


# -> AMI (Amazon Machine Image)

    + Imagem configurada com sistema operacional e aplicativos necessários para inicializar instâncias EC2. Pode ser personalizada ou utilizar imagens padrão fornecidas pela AWS.