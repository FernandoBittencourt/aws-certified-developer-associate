# AWS Certified Developer Associate
## AWS Regions
* A AWS tem regiões ao redor do mundo com nomes "us-east-1", "eu-west-3",...
* Uma região é um cluster (conjunto) de data centers.
* A maioria dos serviços tem escopo de região (region-scoped).
* Os critérios de escolha de uma região pode ser baseado em compliance, proximidade com o cliente, disponibilidade de serviços e preço.
## AWS Availability Zone (AZ)
* Cada região contém zonas de disponibilidade (AZ) com nomes "ap-southeast-2a","ap=southeast-2b".
* Contendo normalmente 3 zonas de disponibilidade por região, sendo o mínimo 2 e o máximo 6.
* Cada AZ é um ou mais datacenters com redundâncias de energia, rede e conectividade. São separados uns dos outros, isolados de desastres.
* Eles são conectados, com redes de alta banda e baixa latência.
## AWS Identity and Access Management (IAM)
* O AWS Identity and Access Management (IAM) é um serviço que ajuda controlar o acesso aos recursos da AWS de forma segura. 
* O IAM serve controlar quem está autenticado (fez login) e autorizado (tem permissões) a utilizar os recursos.
* É um serviço global.
* O Root Account criado por default, não deve ser utilizado e nem compartilhado.
* Os usuários (Users) são pessoas da sua organização que podem ser agrupados. 
* Cada um dos grupos (Groups) só pode conter usuários e não outros grupos.
* Os usuários podem pertencer a múltiplos grupos ou até mesmo a nenhum grupo.
* Alguns serviços da AWS precisam realizar ações a outros serviços da AWS e para isso é preciso incluir permissões com IAM Roles.
* As políticas (Policies) são um documento json que definem as permissões (Permissions) para requisições de serviços na AWS e pode ser usado com ser usado por Users, Groups e Roles. O recomentado é garantir o mínimo de privelegios possivel.
* Uma policy contém um id, uma versão e um ou mais statements (declarações).
* Um Statement em uma IAM policy consiste em Sid (Um identificador), Effect (Allow ou Deny), Principal (account/user/role), Action (lista de ações sobre o recurso), Resource(lista de recursos que a ação será aplicada) e Condition (Condição para que a politica seja válida).
* As boas práticas se segurança sugerem o uso de políticas de password (uso de senhas "fortes") e o uso de autenticação por multi fator (MFA).
* Para acesso programático (CLI/SDK) deve utilizar uma chave de acesso (Access key) gerada e são análogas a uma senha.
* IAM Credentials Report é uma ferramenta de segurança que gera um relatório que lista os usuários de sua conta e o status de suas credenciais, útil para auditoria.
* IAM Access Advisor mostra as permissões de serviço concedidas a um usuário e quando esses serviços foram acessados pela última vez. É possivel usar essas informações para revisar suas políticas.
## Elastic Compute Cloud (EC2)
* Na representação da infraestrutura como um serviço, o EC2 se comporta como uma máquina virtual alugada.
* É possivel definir o sistema operacional, a quantidade de CPU, RAM e o armazenamento, que pode ser conectado a rede (EBS/EFS) ou um hardware (EC2 Instance Store). Definir a rede (velocidade e Ip público), regras de firewall (security group) e um bootstrap script (EC2 User Data, comando de inicialização da máquina).
* É possivel definir o bootstrap script através do EC2 User Data, que é comando que será executado pelo usuário root uma única vez na primeira inicialização. Normalmente contém solicitações de atualização, download de softwares, entre outras dependências.
### Tipos de instâncias (EC2 Instance Types)
* É possivel definir tipos diferentes de instancias otimizadas para atender casos especificos.
* Segue a convenção "m5.2xlarge", sendo m= classe da instância, 5 = geração, 2xlarge = tamanho.
#### Propósito Geral (General Purpose)
* Ótimo para uma diversidade de cargas de trabalho, como servidores da Web ou repositórios de código
* É balanceada entre memoria, cpu e rede.
#### Computação otimizada (Compute Optimized)
* Ótimo para tarefas de computação intensiva que exigem alto desempenho processadores.
#### Memoria Otimizada (Memory Optimized)
* Desempenho rápido para cargas de trabalho que processam grandes conjuntos de dados na memória.
#### Armazenamento otimizado (Storage Optimized)
* Ótimo para tarefas de armazenamento intensivo que exigem alta leitura e gravação sequencial acesso a grandes conjuntos de dados no armazenamento local.
## Security Group
* O Security Group representa um firewalll. Ele controla como o tráfego é permitido dentro ou fora de nossas instâncias do EC2.
* O Security Group contêm apenas regras de permissão (allow rules). Podem ser referenciados por IP ou por um security group.
* Eles regulam o acesso as portas, faixa de ips, controle de rede de entrada (inbound/de outra para a instancia) e de saida (outbound/da instancia para a saida).
* Os security groups podem ser associados a multiplas instancias, restringido em uma combinação de região/VPC.
* Todo o tráfego de entrada é bloqueado por padrão e todo o tráfego de saida é permetido por padrão.
* Problemas de timeout, podem estar associados a um problema de security group. Problemas de connection refused, podem ser associados a um erro da aplicação ou a aplicação não foi iniciada.
## EC2 Instances Purchasing Options
### On-Demand Instances
* Recomendado para cargas de trabalho de curto prazo e ininterruptas. 
* Tem o custo mais alto, mas sem pagamento adiantado. O preço previsível e o pagamento é calculado por segundo.
* Sem compromisso de longo prazo.
### Instâncias reservadas (EC2 Reserved Instances)
* É necessario reservar atributos de instância específicos (tipo de instância, região, locação, sistema operacional)
* É preciso definir um período de reserva, que pode ser 1 ano ou 3 anos. Sendo quanto maior o tempo, maior o desconto.
* As opções de pagamento são sem adiantamento, com adiantamento parcial e com adiantamento total. Sendo a mais barata a que o adiantamento é total e a mais cara sem o adiantamento.
* O escopo da Instância Reservada pode ser Regional or Zonal (capacidade de reserva em uma AZ).
* Recomendado para aplicações de uso em estado estacionário. Por exemplo, um banco de dados.
* Existe uma variação um pouco mais cara, chamada **Convertible Reserved Instance**, ao qual é possivel mudar o tipo de instância, família de instâncias, sistema operacional, escopo e locação.
### EC2 Savings Plans
* Recebe um desconto com base no uso a longo prazo.
* Restrito para uma família de instâncias específica e região da AWS, mas flexível para tamanho da instância, sistema operacional  e locação.
### EC2 Spot Instances
* O mais barato entre todos. (cost-efficient)
* Instâncias que você pode “perder” a qualquer momento se seu preço máximo for menor que o preço spot atual.
* Não deve ser usado para tarefas criticas.
### EC2 Dedicated Hosts
* Um servidor físico com capacidade de instância do EC2 totalmente dedicado ao seu uso.
* Atende aos requisitos de compliance e permite vincular suas licenças de software ao servidor existentes.
* É a opção mais cara entre todos os tipos.
* Para opção de pagamento pode ser por On-Demand ou reservada (1 ou 3 anos).
### EC2 Dedicated Instances
* As instâncias são executadas em hardware que é dedicado à você.
* Pode compartilhar hardware com outros instâncias na mesma conta.
### EC2 Capacity Reservations
* Serve para reservar a capacidade das instâncias sob demanda em uma AZ específica por qualquer duração.
* Nenhum desconto é aplicado para este tipo.
* Adequado para cargas de trabalho ininterruptas de curto prazo que precisam estar em um AZ específico.
## EBS Volume
* Um volume EBS (Elastic Block Store) é uma drive de rede (não é um drive fisico) que você pode anexar para suas instâncias enquanto elas são executadas.
* Permite que suas instâncias persistam dados, mesmo após o término. Funcionando analogamente como um disco.
* Eles só podem ser montados em uma instância por vez, mas uma instancia pode conter mais de um EBS.
* Eles estão vinculados a uma zona de disponibilidade (AZ) específica.
* É possível fazer um backup (snapshot) do EBS. Não é necessario, apesar de recomendado, desanexar o EBS para fazer o snapshot. É possivel copiar o snapshot para outro AZ ou região.
* Por padrão, ao terminar uma instancia EC2 o tipo de root volume será excluído, pois seu atributo "Delete On Termination" é marcado por padrão. Quaisquer outros tipos de volume do EBS não serão excluídos, pois seu atributo "Delete On Termination" está desabilitado por padrão.
### EBS Volume Types
* gp2 / gp3 (SSD): Volume SSD de proposito geral que equilibra preço e desempenho para uma grande variedade de cargas de trabalho.
* io1 / io2 (SSD): Volume SSD de mais alto desempenho para baixa latência ou cargas de trabalho de alto rendimento.
* st1 (HDD): Volume de HDD de baixo custo projetado para cargas de trabalho de alta taxa de transferência acessadas com frequência.
* sc1 (HDD): Volume de HDD de menor custo projetado para cargas de trabalho acessadas com menos frequência.
* Somente gp2/gp3 and io1/io2 (os que são SSD) pode ser usado como "boot volumes".
### EBS Multi-Attach – io1/io2 family
* Anexe o mesmo volume EBS a várias instâncias do EC2 na mesma AZ.
* Cada instância tem permissões leitura e gravação para o volume.
## EC2 Instance Storage
*  EC2 Instance Store são discos de hardware de alto desempenho. Como o EBS tem uma boa performance, mas limitada. O instance storage atende cenarios em que é necessario esse alto desempenho.
*  Melhor desempenho de I/O.
*  Perdem o armazenamento se forem interrompidos, ou seja, existe o risco de perder dados se houver uma falha. São úteis para buffer, cache e outros conteúdos temporários.
## Elastic File System (EFS)
* NFS (network file system) gerenciado que pode ser montado em diversas instancias de EC2 em multi-AZ. Usa o protocolo NFSv4.1.
* Altamente disponível, escalável, caro (3x gp2) e com pagamento por uso.
* Usa o grupo de segurança para controlar o acesso ao EFS.
* Compatível com AMI baseada em Linux (não Windows).
* Criptografia em rest usando KMS.
## Escalabilidade
* Escalabilidade significa que um aplicativo/sistema pode lidar com cargas maiores se adaptando. Existem dois tipos de escalabilidade: vertical e horizontal.
### Escalabilidade vertical
* Escalabilidade vertical significa aumentar o tamanho da instância. Por exemplo, um  aplicativo é executado em um "t2.micro", então executando-o em um t2.large, estaria sendo escalado verticalmente.
* A escalabilidade vertical é muito comum para não sistemas distribuídos, como um banco de dados relacional.
* Geralmente há um limite para o quanto você pode dimensionar verticalmente (limite de hardware).
### Escalabilidade Horizontal
* Escalabilidade Horizontal significa aumentar a número de instâncias/sistemas para uma aplicação.
* A escala horizontal implica em sistemas distribuídos. Sendo muito comum para aplicações web/aplicativos modernos.
## Alta disponibilidade
* A Alta Disponibilidade geralmente "trabalha em conjunto" com a escala horizontal.
* Alta disponibilidade significa executar o aplicativo/sistema em pelo menos 2 data centers (AZ). O objetivo da alta disponibilidade é sobreviver a uma perda de um dos data centers.
* A alta disponibilidade pode ser passiva (RDS Multi AZ por exemplo) ou ativa (por escala horizontal).
## Load Balances
* Load Balances são servidores que encaminham tráfego para vários outros servidores (por exemplo, instâncias EC2).
### Vantagens
* Distribue a carga em várias instâncias. Portanto, lida com falhas de instâncias, criando alta disponibilidade entre zonas.
* Expoem um único ponto de acesso (DNS) ao seu aplicativo.
* Realiza verificações regulares de integridade de suas instâncias.
* Fornece SSL (HTTPS) para seus sites.
* Reforça a aderência com cookies.
* Separa o tráfego público do tráfego privado.
### Elastic Load Balancer
* O Elastic Load Balancer é um balanceador de carga gerenciado, ou seja, a AWS garante que funcionará, sendo responsabilidade dela cuidar de atualizações, manutenção, alta disponibilidade, permitindo apenas a configuração pelo usuário.
* É integrado a muitos serviços da AWS como EC2 Auto Scaling Groups, EC2, Amazon ECS, AWS Certificate Manager (ACM), CloudWatch, Route 53, AWS WAF, AWS Global Accelerator.
### Health Checks
* As verificações de integridade (Health Checks) são cruciais para balanceadores de carga. Eles permitem que o balanceador de carga saiba se as instâncias para as quais ele encaminha tráfego estão disponíveis para responder às solicitações.
* A verificação de integridade é feita em uma porta e uma rota (/health, é a comum). Se a resposta não for 200 (OK), a instância não está íntegra.
### Tipos de load balancer
* Existem 4 tipos de load balancers.
* No geral, é recomendável usar os balanceadores de carga de geração mais recente, pois eles fornecem mais recursos.
* Alguns balanceadores de carga podem ser configurados como internos (privados) ou externos (públicos).
#### Classic Load Balancer (v1 - old generation) – 2009 – CLB
* Suporta TCP (Layer 4), HTTP & HTTPS (Layer 7).
* Health checks são baseados TCP ou HTTP.
* Hostname fixo: XXX.region.elb.amazonaws.com.
#### Application Load Balancer (v2 - new generation) – 2016 – ALB 
* Application load balancers é camada 7 (HTTP).
* Balanceamento de carga para vários aplicativos em máquinas diferentes (target groups).
* Balanceamento de carga para vários aplicativos na mesma máquina (ex: containers).
* Suporte para HTTP/2 e WebSocket.
* Suporte a redirecionamentos (de HTTP para HTTPS, por exemplo).
* Encaminha tabelas para diferentes target groups. 
  * Roteamento baseado no caminho na URL (example.com/users & example.com/posts). 
  * Roteamento baseado no nome do host na URL (one.example.com & other.example.com).
  * Roteamento baseado em Query String, Headers (example.com/users?id=123&order=false).
  * O ALB é uma ótima opção para micro serviços e aplicativos baseados em contêiner (exemplo: Docker e Amazon ECS). Tem um recurso de mapeamento de porta para redirecionar para uma porta dinâmica no ECS.
* Hostname Fixo: XXX.region.elb.amazonaws.com.
* Os servidores de aplicativos não veem o IP do cliente diretamente, sendo que o Ip verdadeiro vem no header X-Forwarded-For. é possivel também obter a porta (X-Forwarded-Port) e o proto (X-Forwarded-Proto).
##### Target Group
* Instâncias do EC2 (podem ser gerenciadas por um Auto Scaling Group) – HTTP.
* Tasks do ECS (gerenciadas pelo próprio ECS) – HTTP.
* Para as funções Lambda a solicitação HTTP é traduzida em um evento JSON.
* Endereços IP devem ser IPs privados.
* ALB pode rotear para vários Target Groups.
* As health checks estão no nível do Target Group.
#### Network Load Balancer (v2 - new generation) – 2017 – NLB
* Os balanceadores de carga de rede (camada 4) permitem encaminhe o tráfego TCP e UDP para suas instâncias, lidar com milhões de solicitações por segundo e tem menos latência ~ 100 ms (vs 400 ms para ALB).
* O NLB tem um IP estático por AZ e oferece suporte à atribuição de IP elástico (útil para colocar IP específico na lista de permissões).
* NLB are used for extreme performance, TCP or UDP traffic.
* Os Target Groups podem ser instâncias EC2, endereços IP privados ou Application Load Balancer.
#### Gateway Load Balancer – 2020 – GWLB
* Opera na camada 3 (Network layer) – IP Protocol
* Permite implantar, dimensionar e gerenciar um conjunto de dispositivos de rede virtuais de terceiros na AWS. Exemplos: Firewalls, Sistemas de detecção de Intrusão e de prevenção, Sistemas de inspeção profunda de pacotes, manipulação de carga, etc.
* Combina as seguintes funcionalidades: Transparent Network Gateway (entrada/saída única para todo o tráfego) e  Load Balancer (distribui o tráfego para seus dispositivos virtuais).
* Usa o protocolo GENEVE na porta 6081.
### Sticky Sessions (Session Affinity)
* É possível implementar a stickiness para que o mesmo cliente seja sempre redirecionado para a mesma instância por trás de um Load Balancer.
* Isso funciona para Classic Load Balancers e para Application Load Balancers.
* O "cookie" usado para aderência tem uma data de validade (expiration date) que você controla.
* Caso de uso: garantir de que o usuário não perca seu dados da sessão.
* Habilitar a stickiness pode trazer desequilíbrio de carga nas instâncias do EC2 de back-end, ou seja, muitas rqeuisições na mesma instancia, enquanto poucas em outras.
#### Cookie Names
* Application-based Cookies
 * Custom cookie
  * Gerado pelo target.
  * Pode incluir quaisquer atributos personalizados exigidos pelo aplicativo.
  * O nome do cookie deve ser especificado individualmente para cada target group.
  * Não deve usar os nomes AWSALB, AWSALBAPP ou AWSALBTG, pois são reservados para uso pelo ELB.
 * Application cookie
  * Cookie gerado pelo load balancer.
  * O nome do cookie é AWSALBAPP.
* Duration-based Cookies
 * Cookie gerado pelo load balancer.
 * O nome do cookie é AWSALB para ALB e AWSELB para CLB.
### Cross-Zone Load Balancing
* Balanceamento de cargas entre AZ. Os nós do Load balancer distribuem solicitações de clientes para targets registrados. Quando o balanceamento de carga entre zonas (cross-zone load balancing) está habilitado, cada nó do balanceador de carga distribui o tráfego entre os todos targets registrados em todas as AZ habilitadas, ou seja a distruibuição passa a ser por instancia independente da AZ. Quando o balanceamento de carga entre zonas está desabilitado, cada nó do balanceador de carga distribui o tráfego apenas entre os targets em sua zona de disponibilidade, nesse caso a distruibuição passa a ser por AZ. 
* Sempre ativo para o Application Load Balancer, não pode ser desabilitado e não gera cobranças  para dados entre AZ.
* Desabilitado por padrão para o Network Load Balancer e *gera* cobranças para dados entre AZ, se habilitado.
* Desabilitado por padrão para o Network Load Balancer e mas *não gera* cobranças para dados entre AZ, se habilitado.
### SSL/TLS
* Um certificado SSL permite o tráfego entre seus clientes e seu balanceador de carga a ser criptografado em trânsito (in-flight encryption).
* SSL refere-se a Secure Sockets Layer, usado para criptografar conexões. TLS refere-se ao Transport Layer Security, que é uma versão mais recente. Os certificados TLS são mais usados, mas as pessoas ainda se referem a eles como SSL.
* Os certificados SSL públicos são emitidos por Autoridades de Certificação (CA).
* Os certificados SSL têm uma data de expiração (definida por você) e devem ser renovados.
* Balanceador de carga usa um certificado X.509 (certificado de servidor SSL/TLS).
* Você pode gerenciar certificados usando o ACM (AWS Certificate Manager) e você pode fazer upload de seus próprios certificados alternativamente.
#### Server Name Indication (SNI)
* O SNI resolve o problema de carregar vários certificados SSL em um servidor web (para atender a vários sites).
* É um protocolo “mais recente” e exige que o cliente para indique o hostname do servidor de destino no handshake SSL inicial. O servidor irá então encontrar o certificado correto, ou retornar o default.
* Só funciona para ALB e NLB (mais recentegeração) e para o CloudFront.
### Connection Draining / Deregistration Delay
* Connection Draining para CLB e Deregistration Delay para ALB e NLB.
* É um tempo para completar “in-flight requests” enquanto o a instância está de-registering ou unhealthy. Ou seja, é um tempo para o servidor atender as requisições que foram feitas a ele, antes de se desregistrar.
* Interrompe o envio de novas solicitações para o EC2 instância que está cancelando o registro.
* Entre 1 a 3600 segundos (default: 300 segundos), pode ser desabilitado definindo o valor como 0. Recomendado definir um valor baixo se suas requisições forem curtas.
## Auto Scaling Group (ASG)
* O objetivo de um Auto Scaling Group (ASG) é:
 * Escalar horizontalmente, adicionando instâncias do EC2 para atender a uma carga maior e removendo instâncias do EC2 para atender a uma carga reduzida.
 * Definir um número mínimo e máximo de instâncias do EC2 em execução.
 * Regitrar automaticamente novas instâncias em um balanceador de carga.
 * Recriar uma instância do EC2 caso uma anterior seja encerrada (ex: se não estiver íntegra).
 * Boas métricas para escalar :
   * CPUUtilization: CPU média utilização em suas instâncias.
   * RequestCountPerTarget: para ter certeza se o número de solicitações por EC2 instâncias é estável.
   * Average Network In / Out: Média de entrada/saída de rede (se você estiver aplicativo está vinculado à rede).
   * Qualquer métrica personalizada que você envia usando o CloudWatch.
### Auto Scaling - CloudWatch Alarms & Scaling
* É possível dimensionar um ASG com base em alarmes do CloudWatch.
* Um alarme monitora uma métrica (como CPU média ou uma métrica personalizada). Métricas como CPU média são calculadas para as instâncias do ASG.
* Com base no alarme: Podemos criar políticas de expansão (aumentar o número de instâncias) e criar políticas de redução (diminuir o número de instâncias).
#### Dynamic Scaling Policies
* *Target Tracking Scaling*: Mais simples e fácil de configurar. Exemplo: Quero que a CPU média do ASG fique em torno de 40%.
* *Simple / Step Scaling*: Regras como quando um alarme do CloudWatch é acionado (por exemplo, CPU > 70%), adicione 2 unidades. Quando um alarme do CloudWatch é acionado (por exemplo, CPU < 30%), remova 1.
* *Scheduled Actions*: Antecipar um dimensionamento com base em padrões de uso conhecidos. Exemplo: aumentar a capacidade mínima para 10 às 17h às sextas-feiras.
#### Predictive Scaling
* Prever continuamente a carga e programar o escalonamento com antecedência.
### Scaling Cooldowns
* Depois que uma atividade de dimensionamento acontece, ocorre o período de espera (cooldown). Sendo que que o default é 300 segundos.
* Durante o período de cooldown, o ASG não inicia instâncias adicionais ou encerra (para permitir que as métricas se estabilizem)
* Conselho: Use uma AMI pronta para usar para reduzir o tempo de configuração e atender as requisições mais rápidos e reduzir o período de cooldown.
## Relational Database Service (RDS)
* É um serviço de banco de dados gerenciado para banco de dados que usa SQL como linguagem de consulta.
* Permite criar bancos de dados na nuvem gerenciados pela AWS e são eles: Postgres, MySQL, MariaDB, Oracle, Microsoft SQL Server e Aurora (banco de dados proprietário da AWS).
* O RDS é um serviço gerenciado e ele fornece: 
 * Provisionamento automatizado e patch de sistema operacional.
 * Backups contínuos e restauração para um timestamp específico (Point in Time Restore).
 * Painéis de monitoramento.
 * Réplicas de leitura para melhor desempenho de leitura.
 * Configuração Multi AZ para DR (Recuperação de Desastres/ Disaster Recovery).
 * Janelas de manutenção para atualizações.
 * Capacidade de dimensionamento (vertical e horizontal).
 * Armazenamento suportado por EBS (gp2 ou io1).
* Não é possível fazer SSH para as instâncias.
### RDS Backups
* Os backups são ativados automaticamente no RDS.
* Backup Automatizado:
 * Backup completo diário do banco de dados (durante a janela de manutenção).
 * Os logs de transações são copiados pelo RDS a cada 5 minutos, capacidade de restaurar a qualquer momento (do backup mais antigo até 5 minutos atrás)
 * Tem 7 dias de retenção (pode ser aumentado para 35 dias).
* DB Snapshots:
 * Acionado manualmente pelo usuário.
 * Retenção de backup pelo tempo que o usuário quiser.
### Storage Auto Scaling
* Ajuda a aumentar o armazenamento de uma instância de banco de dados RDS dinamicamente.
* Quando o RDS detecta que você está ficando sem banco de dados gratuito armazenamento, ele é dimensionado automaticamente.
* Deve ser evitado dimensionar manualmente o armazenamento do banco de dados.
* Você precisa definir o Maximum Storage Threshold (limite máximo para armazenamento de banco de dados).
* Útil para aplicativos com cargas de trabalho imprevisíveis.
* Suporta todos os mecanismos de banco de dados RDS (MariaDB, MySQL, PostgreSQL, SQL Server, Oracle).
### RDS Read Replicas
* Até 5 réplicas de leitura (Read Replicas).
* Dentro da AZ, Cross AZ (Entre Az) ou Cross Region (Entre regiões).
* A replicação é assincrona, então as leituras são eventualmente consistente (eventually consistent).
* As réplicas podem ser promovidas a seu próprio banco de dados.
* As réplicas de leitura são usadas para apenas para consultas (SELECT), ou seja, não deve modificar os dados (INSERT, UPDATE, DELETE).
### Network Cost
* Na AWS há um custo de rede quando os dados vão de uma AZ para outra.
* Para RDS Read Replicas na mesma região, você não paga essa taxa.
### RDS Multi AZ (Disaster Recovery)
* A replicação é sincrona.
* Um único nome DNS, ou seja, failover automático do aplicativo, o mesmo nome é usado em caso de falha.
* Aumenta a disponibilidade, mas não é usado para escalabilidade.
* Tolerancia a falhas (Failover) em caso de perda de AZ, de rede, instância ou armazenamento. Sem intervenção manual em aplicativos.
* As Réplicas de Leitura devem ser configuradas como Multi AZ para recuperação de desastres (DR). A replicação Multi-AZ é gratuita.
#### De Single-AZ para Multi-AZ
* Zero downtime operation (não precisa parar o DB), basta clicar em modify.
* O seguinte acontece internamente: Uma snapshot é gerada, Um novo banco de dados é restaurado da snapshot em uma nova AZ e a sincronização é estabelecida entre os dois bancos de dados.
### RDS Security
* Criptografia em REST:
 * Possibilidade de criptografar o master e as read replicas com AWS KMS, criptografia em AES-256. Sendo que A criptografia deve ser definida no momento do lançamento.
 * Se o master não estiver criptografado, as réplicas de leitura não podem ser criptografadas.
 * Transparent Data Encryption (TDE) disponível para Oracle e SQL Server.
* In-flight encryption:
 * Certificados SSL para criptografar dados para RDS em trânsito.
 * Fornece opções de SSL com certificado de confiança ao se conectar ao banco de dados.
 #### Network Security
 * Os bancos de dados RDS geralmente são implantados em uma sub-rede privada, não em uma pública.
 * A segurança do RDS funciona aproveitando security groups (o mesmo conceito do EC2), controlando qual IP ou security group pode se comunicar com o RDS.
 #### Access Management
 * As políticas do IAM ajudam a controlar quem pode gerenciar o AWS RDS (por meio da API do RDS).
 * Nome de usuário e senha tradicionais podem ser usados para fazer login no banco de dados.
 * A autenticação baseada em IAM pode ser usada para fazer login no RDS MySQL e PostgreSQL.
 ## Amazon Aurora
 * Aurora é uma tecnologia proprietária da AWS (não de código aberto).
 * Postgres e MySQL são suportados como Aurora DB (isso significa que seu drivers funcionarão como se o Aurora fosse um banco de dados Postgres ou MySQL).
 * O Aurora é “otimizado para a nuvem da AWS” e reivindica uma melhoria de desempenho de 5x sobre MySQL no RDS, mais de 3x o desempenho do Postgres no RDS.
 * O armazenamento Aurora cresce automaticamente em incrementos de 10 GB, até 128 TB.
 * O Aurora pode ter 15 réplicas enquanto o MySQL tem 5 e o processo de replicação é mais rápido (atraso de réplica de menos de 10 ms).
 * O failover no Aurora é instantâneo, ou seja, a alta disponibilidade é nativa.
 * Aurora custa mais que RDS (20% a mais), mas é mais eficiente.
 ## ElastiCache
 * Da mesma forma que o RDS é para obter bancos de dados relacionais gerenciados, ElastiCache é obter Redis ou Memcached gerenciado.
 * Caches são bancos de dados na memória com desempenho realmente alto e baixa latência.
 * Ajuda a reduzir a carga de bancos de dados para cargas de trabalho de leitura intensa.
 * Ajuda a tornar a aplicação *stateless*.
 * A AWS cuida da manutenção/aplicação de patches do sistema operacional, otimizações, configuração, monitoramento, recuperação de falhas e backups.
 * O uso do ElastiCache envolve mudanças pesadas no código do aplicativo.
 * Em relação ao uso como cache a consultas de banco de dados por aplicações, se não disponível no ElastiCache, obter de RDS e armazenar no ElastiCache. O cache deve ter uma estratégia de invalidação para certificar que apenas os dados mais atuais sejam obtidos de lá.
 * Em relação ao uso como sessão de usuário, o usuário faz login em qualquer uma das aplicações e a aplicação grava os dados da sessão no ElastiCache. Se a requisição chegar em outra instância da aplicação, a instância recupera os dados e o usuário continua logado nela.
 ### Redis
 * Multi-AZ com Failover Automático.
 * Replicas de leitura com objetivo de escalar a leitura e prover a alta disponibilidade.
 * Durabilidade dos dados usando AOF persistência.
 * Recursos de backup e restauração.
 ### Memcached
 * Multi-node para particionamento dedados (sharding).
 * Sem alta disponibilidade (replicação).
 * Sem persistência.
 * Sem recursos de backup e restauração.
 * Multi-threaded architecture.
### ElastiCache – Cache Security
* Não suporta autenticação do IAM
* As políticas do IAM no ElastiCache são usadas apenas para segurança no nível da API da AWS.
* Redis AUTH
 * É possivel definir uma “senha/token” quando criar um cluster Redis.
 * Este é um nível extra de segurança para seu cache (em cima dos grupos de segurança).
 * Suporte a criptografia SSL.
* Memcached
 * Suporta autenticação baseada em SASL (avançada).
### ElastiCache Replication
#### Cluster Mode Disabled
* Um nó primário e até 5 réplicas.
* Replicação assincrona.
* O nó primário é usado para leitura/gravação e os outros nós são somente leitura.
* Um shard, todos os nós têm todos os dados.
* Proteje contra perda de dados em caso de falha do nó.
* Multi-AZ habilitado por padrão para failover.
* Útil para escalar o desempenho de leitura.
#### Cluster Mode Enabled
* Os dados são particionados em shards (útil para escalar gravações).
* Cada fragmento tem um primário e até 5 nós de réplica (mesmo conceito de antes).
* Capacidade multi-AZ.
### Design patters de cache
* *Lazy Loading / Cache-Aside / Lazy Population* (Só atualiza o cache na consulta)
 * Prós
  * Apenas os dados solicitados são em cache (o cache não está preenchido com dados não utilizados).
  * Falhas de nós não são fatais (apenas aumento da latência para aquecer a cache).
 * Contras
  * Penalidade de falta de cache que resulta em 3 viagens de ida e volta, atraso perceptível para essa solicitação.
  * Dados obsoletos: os dados podem ser atualizados no banco de dados e desatualizado no cache.
* *Write Through* (Adicionar ou atualizar o cache quando o banco de dados for atualizado)
 * Prós
  * Os dados em cache nunca são obsoleto, as leituras são rápidas.
  * Penalidade de gravação vs leitura penalidade (cada gravação requer 2 chamadas)
 * Contras
  * Dados ausentes até que sejam adicionados/atualizados no banco de dados. A mitigação é implementar a estratégia Lazy Loading também.
  * Cache churn, muitos dos dados nunca serão lidos.
### Cache Evictions and Time-to-live (TTL)
* O *Cache eviction* (despejo de cache) pode ocorrer de três maneiras:
 * Você exclui o item explicitamente no cache.
 * O item é despejado porque a memória está cheia e não foi usada recentemente (LRU).
 * Você define o time-to-live (Tempo de vida)de um item (ou TTL).
* Se ocorrerem muitos despejos devido à memória, você deve aumentar ou diminuir a escala
