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
* As políticas (Policies) são um documento json que contém as permissões (Permissions) de usuários ou grupos.
* Alguns serviços da AWS precisam realizar ações e para é preciso incluir permissões com IAM Roles.
* As boas práticas se segurança sugerem o uso de políticas de password (uso de senhas "fortes") e o uso de autenticação por multi fator (MFA).
* Para acesso programático (CLI/SDK) deve utilizar uma chave de acesso (Access key) gerada e são análogas a uma senha.
* IAM Credentials Report é um relatório que lista os usuários de sua conta e o status de suas credenciais, útil para auditoria.
* IAM Access Advisor mostra as permissões de serviço concedidas a um usuário e quando esses serviços foram acessados pela última vez. É possivel usar essas informações para revisar suas políticas.
