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
        -> Quem está logado, apenas deve acessar aqyulo que deveria ver.
