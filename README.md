# Relatório de Implementação de Serviços AWS para Redução de Custos e Melhoria da Arquitetura

## 1. Introdução

Este relatório descreve a estratégia para a redução de custos e a melhoria da arquitetura da Farmácia São João, que atualmente opera com uma aplicação monolítica em servidores convencionais e integrações de APIs externas com alto acoplamento. O objetivo é implementar soluções baseadas em AWS para otimizar o uso dos recursos, reduzir despesas e melhorar a arquitetura da aplicação utilizando Amazon SQS para desacoplamento.

## 2. Análise Atual

### 2.1. Infraestrutura Atual

- **Servidores e Aplicações**: A farmácia utiliza servidores físicos locais para hospedar uma aplicação monolítica que gerencia inventário, vendas, e dados de clientes. A aplicação possui alta integração com APIs externas para processamento de pagamentos e serviços de terceiros.
- **Custos Atuais**: Os custos mensais de manutenção dos servidores são aproximadamente R$ 10.000, com despesas adicionais relacionadas a licenças de software e consumo de energia.
- **Problemas Identificados**: 
  - **Capacidade limitada e custo elevado** com manutenção de hardware.
  - **Baixa escalabilidade** e dificuldade em lidar com picos de demanda.
  - **Altamente acoplada com APIs externas**, tornando a manutenção e escalabilidade da aplicação desafiadoras.

## 3. Estratégias de Redução de Custos e Melhoria da Arquitetura

### 3.1. Otimização de Recursos

#### 3.1.1. **Migração para Instâncias EC2**

- **Instâncias Reservadas**: Adquirir instâncias EC2 reservadas (por exemplo, m5.large) para aplicações críticas, aproveitando descontos de até 30% em comparação com o modelo sob demanda.
- **Savings Plans**: Implementar Savings Plans para flexibilidade adicional e economias em serviços de computação.

#### 3.1.2. **Uso de Instâncias Spot**

- **Instâncias Spot**: Utilizar instâncias Spot para cargas de trabalho flexíveis e não contínuas, reduzindo custos de computação em até 90%.

### 3.2. Armazenamento Eficiente

#### 3.2.1. **Armazenamento em Amazon S3**

- **Classificação de Dados**: Migrar backups e dados históricos para o Amazon S3, aplicando políticas de ciclo de vida para mover dados menos acessados para S3 Glacier.
- **Economias Esperadas**: Reduzir custos de armazenamento em até 50% em comparação com soluções físicas.

#### 3.2.2. **Volume EBS**

- **Volume EBS Otimizado**: Para as instâncias EC2, utilizar volumes EBS otimizados para throughput (st1) para grandes transferências de dados.

### 3.3. Melhoria da Arquitetura com Amazon SQS

#### 3.3.1. **Desacoplamento com Amazon SQS**

- **Amazon SQS**: Implementar Amazon SQS para desacoplar a aplicação monolítica das APIs externas. Isso permitirá que a aplicação envie e receba mensagens de forma assíncrona, reduzindo o impacto de falhas nas APIs externas e melhorando a escalabilidade.
- **Benefícios Esperados**: 
  - **Redução do acoplamento**: A aplicação não precisa esperar pela resposta das APIs externas, melhorando a robustez e a escalabilidade.
  - **Aumento da Resiliência**: Mensagens podem ser processadas em momentos diferentes, aumentando a capacidade de lidar com picos de carga.

### 3.4. Gestão e Monitoramento

#### 3.4.1. **Monitoramento e Alarmes**

- **AWS CloudWatch**: Configurar monitoramento e alarmes para acompanhar o uso de recursos e otimizar a alocação de capacidade.
- **AWS Cost Explorer**: Utilizar o Cost Explorer para analisar despesas e identificar oportunidades de economia.

#### 3.4.2. **Automação de Escalabilidade**

- **Auto Scaling**: Configurar Auto Scaling para ajustar a capacidade das instâncias EC2 de acordo com a demanda.

### 3.5. Rede e Segurança

#### 3.5.1. **Otimização de Dados de Rede**

- **Amazon CloudFront**: Implementar CloudFront para reduzir a latência e o custo de transferência de dados, especialmente se a farmácia tiver uma presença online.

#### 3.5.2. **AWS WAF e Shield**

- **AWS WAF**: Implementar WAF para proteger a aplicação contra ataques e tráfego malicioso.
- **AWS Shield**: Utilizar proteção adicional contra DDoS para garantir a disponibilidade.

## 4. Implementação

### 4.1. Plano de Ação

1. **Análise Detalhada**: Conduzir uma análise detalhada da infraestrutura atual e definir requisitos para a migração para a AWS.
2. **Migração para EC2 e EBS**: Planejar e executar a migração das aplicações para instâncias EC2 e configurar volumes EBS para atender às necessidades de armazenamento e processamento.
3. **Implementação de Armazenamento em S3**: Migrar dados e backups para Amazon S3 e configurar políticas de ciclo de vida.
4. **Implementação do Amazon SQS**: Configurar e integrar o Amazon SQS para desacoplar a aplicação das APIs externas e melhorar a escalabilidade.
5. **Configuração de Monitoramento e Escalabilidade**: Implementar monitoramento com CloudWatch e configurar Auto Scaling.
6. **Otimização de Rede e Segurança**: Configurar CloudFront, AWS WAF e Shield.

### 4.2. Cronograma

- **Semana 1-2**: Análise detalhada e planejamento da migração.
- **Semana 3-4**: Migração para instâncias EC2 e configuração de EBS.
- **Semana 5-6**: Implementação de armazenamento em Amazon S3 e configuração do Amazon SQS.
- **Semana 7-8**: Configuração de monitoramento e escalabilidade, e otimização de rede e segurança.

## 5. Conclusão

A implementação das estratégias propostas visa reduzir os custos operacionais da Farmácia São João e melhorar a arquitetura da aplicação ao migrar para uma infraestrutura em nuvem mais escalável e eficiente. A adoção de soluções AWS, incluindo Amazon SQS para desacoplamento, proporcionará economias significativas, maior flexibilidade e uma gestão mais eficaz dos recursos.
