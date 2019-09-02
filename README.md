
# Z-Tech Challenge

## Arquitetura - Diagrama AWS

O diagrama abaixo representa uma infraestrutura na cloud AWS. A proposta elaborada é relativamente simples, mas capaz de atender os requisitos apresentados no desafio.

![Diagrama AWS](https://i.ibb.co/gSCG8ww/z-tech.png)

* Route 53 para o gerencionamento DNS, com RecordSet apontando através de um alias para o ELB
* O ELB está balanceado a carga entre instâncias EC2 (min 2) atreladas a uma regra de auto-scaling
* As instâncias EC2 estão apontando para um volume (EBS) apartado do cluster
* O RDS (MySQL) está permitindo requisições apenas das instâncias do cluster, configurado através de grupo de segurança


## IaC - AWS CloudFormation

O arquivo `z-tech-cloudformation.json` contém o script necessário para provisionar a infraestrutura proposta no diagrama acima, através do CloudFormation da AWS.


## Observações importantes

* Para a questão da sessão em disco, minha sugestão é persistir a sessão em banco de dados (exemplo de config: [https://culttt.com/2013/02/04/how-to-save-php-sessions-to-a-database/](https://culttt.com/2013/02/04/how-to-save-php-sessions-to-a-database/)), usando o próprio RDS do diagrama.

* Para o armazenamento está sendo considerado o AWS EBS Elastic Volume (doc: [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modify-volume.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modify-volume.html)), garatindo assim o escale automático do size.

