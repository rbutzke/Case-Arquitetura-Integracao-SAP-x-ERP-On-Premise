# Case-Arquitetura-Integracao-SAP-x-ERP-On-Premise
Case Arquitetura Integracao SAP x ERP On Premise

## Resumo Executivo

| Campo | Descrição |
|-------|-----------|
| **PROJETO** | Integração SAP ECC (On Premise) x ERP Nacional (On Premise) |
| **DESAFIO** | SOAP (SAP) vs REST (ERP) - protocolos incompatíveis |
| **SOLUÇÃO** | Integrador com conversão REST → SOAP operando no KS |
| **VOLUMETRIA** | 350 mil registros/semana (capacidade calculada: 362k) |
| **ARQUITETURA** | KS + hardware xxxx + RabbitMQ DLQ + PostgreSQL Master/Slave |
| **DIFERENCIAIS** | Batch adaptativo, Dead Letter Queue, Persistent Volume |
| **CUSTO MENSAL** | US$ 218 (EKS + EC2 + EBS) + US$ 80 (IA Cloud) |
| **PRAZO ESTIMADO** | 8 a 12 semanas (Em meses: aproximadamente 2 a 3 meses) | 
| **METODOLOGIA** | Scrum + SOLID + Arquitetura do Framework escolhido | 




## Contexto de Negócio

A empresa XYZ hoje utiliza somente o SAP ECC , existe a necessidade de integrar Contábil , Financeiro , Jurídico e RH vindos do ERP Nacional recem adquirido.

Este projeto visa integrar Contábil , Fiscal , Juridico e RH provenientes do ERP Nacional para o SAP ECC. 


## Cenário Atual

SAP ECC se encontra em ambiente On Premise na empresa XYZ em uma DMZ , operando com exposição de webservices SOAP . 

O ERP Nacional se encontra On Premise na Empresa XYZ porém em outro servidor e outra DMZ, operando com expisução de APIs Rest não suportando requisições SOAP. 


Mediante este cenário será construído um integrador ao qual deverá viabilizar a questão da incompatibilidade existe ECC(webservice SOAP) x ERP Nacional(API Rest) 

Ja existe um FrontEnd (em Vue.js de monitoramento e manipulação do integrador)criado pelo time da empresa XYZ que se encontra hospedado em outro servidor e outra DMZ , o integrador deverá ser construído com base nos contratos desse FrontEnd já existe.


## Metodologia Aplicada ao Desenvolvimento:

Para criação do Integrador deverá ser utilizada a metologia SOLID , respeitando o funcionamento do Framework/tecnologia escolhida sem descaracterizar as mesmas.

SpringBoot implementa:  

Arquitetura em Camadas (tradicional) 
Camada de Apresentação/Controladores (Presentation/Controller Layer)


ou 

Arquitetura Hexagonal (Port e Adpters).


FastAPI

NestJS



Ferramenta de Apoio na Utlização do SDD:  

https://github.com/github/spec-kit

Dentro deste contexto se faz necessário o uso de IA para apoio no processo de desenvolvimento, não sendo o objetio fazer "VibeCode" mas sim utilizar como ferramenta de apoio no processo de desenvolvimento.


## Sugestão de IA Cloud 

| Componente | Especificação | Custo |
|------------|----------------|----|
| Minimax 2.7 | 1 Trilhão de parametros ,4500 requisições a cada 5 horas | 20 dolares mensal |

https://platform.minimax.io/subscribe/token-plan

## Custo Estimado  

4 Usuários a 20 mensal = 80 Dolares mês


## Configuração do LLM On Premise (para cenário com restrições de segurança/LGPD)

| Componente | Especificação | Custo |
|------------|----------------|----|
| Processador | Intel i7 14700 com 20 núcleos e 28 threads | 2600 |
| Water Cooler | Corsair Nautilus 360 mm | 800 |
| Placa Mãe | Asus Z790 PRO com suporte a Bifurcação | 2000 |
| Memória RAM | 4x 32GB DDR5 6000Hz (total 128GB) | 8000 |
| Placa de Vídeo | 1x RTX 5090 32GB ou 2x RTX 5060 TI 16GB | RTX5090 = 26999 , RTX5060TI = 3500 | 
| Fonte | Corsair 1200W Gold | 1500 |
| SSD | Adata Legend 860, 2TB, M.2 2280 | 1500 |
| Gabinete | Corsair Obsidian 1000D ou Estação para rigs de mineração | Obsidian=1700 ou Estação=500 |
| Fans | Cosair 20x de 120mm |1000 |
| Fans | Corsair  4x de 140mm  | 400 |



## Custo Estimado do Setup 

 Utilizando 1 RTX 5090 = 46.499

 Utilizando 2 RTX 5060 TI = 26.500
  

## Harness 

Hermes Agent 
Possui memoria e aprende com o uso , um dos melhores do mercado 

https://github.com/nousresearch/hermes-agent


OpenCode  
O mais utilizado na Comunidade Open Source

https://opencode.ai/

## Modelos
  
Qwen3.6 35b a3e 
Arquitetura(Moe) 23g quantizado em Q4-K-M com contexto de 262k indicado para codificação , chamada de ferramentas, geração de diagramas , visão , extremamente rapido , entrega em torno de 100 tokens   

https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF

Modelo Qwen3.6 27b 
Arquitetura (Densa) 17g quantizado em Q4-K-M com contexto de 262k indicado para codificação, raciocinio profundo , geração de diagramas , visão ,modelo lento mas extremamente inteligente, entrega em torno de 21 tokens com MTP ativo entrega 44 tokens porém aumenta o consumo de RAM

https://huggingface.co/unsloth/Qwen3.6-27B-GGUF

Suporte a MTP

https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF


## Mecanismos de Inferencia 

LLAMA.CPP focado principalmente em performance , consegue extrair máxima performance do hardware/modelo suporta até 4 usuários simultaneos , mas pode apresentar pequenas instabilidades nestas configs de multi users.

https://github.com/ggml-org/llama.cpp


VLLAMA não tão focado em performance e simplicidade mas sim focado principalmente em multi users consegue suportar vários usuarios simultaneos   

https://github.com/erkkimon/vllama


## EKS + EC2 Custo Computacional

Custo do Plano de Controle (EKS Cluster) - US$ 0,10 por hora, versão Standart do Kubernets.  

US$ 0,10 x 24 Horas x 30 dias = US$ 73,00

Custo da Computação (Onde os Pods Rodam) m6i.xlarge 24/7 

| Componente | Especificação | 
|------|-------|
| 4 vCPUs | 2 cores físicos com 2 threads cada |
| Memória RAM | 16G |
| Processador |  Intel Xeon 8375C (Ice Lake) com até 3.5 GHz e suporte a AVX-512 |
| Rede |  Largura de banda de até 10 Gbps |
| Armazenamento | gp2 |  

Região us-east-1 AWS localizada no Norte da Virgínia, Estados Unidos , mais antiga e que possui multiplas Zonas de Disponibilidade para redundância dentro da própria região.  




Sob Demanda (On-Demand)	US$ 0,20  

US$ 0,20 × 720h	= US$ 144,00

A m6i.xlarge suporta 48 pods

Para este plano é contemplado o Provisioned Control Plane Standart

Para o Rabbitmq para o Persistent Volume será necessário 10 GB de armazenamento persistente (EBS na AWS)

10GB x US 0,10 = US 1,00.

Custo estimado: US$ 1.00 por mês (gp2 volume).

Custo total: 73.00	+ US$ 144.0 + US$ 1.00 = US$ 218 mensal 

## Periodicidade 
Será conforme demanda dos Sistemas SAP ECC x ERP Nacional


## Latência 
As Arquiteturas SOAP e REST poderão apresentar resposta variável não sendo possivel resposta instantanea , fatores como volumetria enviada , rede , proxys/dns , operadora de internet poderão interferir nestes retornos.


## Volumetria
Estimativa de 200 a 350 mil registros por semana

Capacidade com 3 Consumers (cenário atual)

Tempo por mensagem: 5 segundos  

Mensagens por minuto por Consumer: 60 ÷ 5 = 12 msg/min  

Mensagens por hora por Consumer: 12 × 60 = 720 msg/hora  


3 Consumers = 720 × 3 = 2.160 mensagens/hora  

2.160 × 24 horas = 51.840 mensagens/dia  

51.840 × 7 dias = 362.880 mensagens/semana  


## Infra utilizada:

| Descritivo | Local | Responsavel | 
|----|------|-----------|
|SAP ECC | On Premise | SAP|
|Integrador | AWS Cloud | Time do Projeto |
|ERP Nacional | IBM Cloud | Nacional |


## Tecnologias:

| Tecnologia | Distribuidor | 
|----|-----------|
|SAP ECC | SAP |
|Python | Python Software Foundation (PSF)| 
|FastAPI | Scalar.com |
| Pip | Python Packaging Authority |
|Java | Oracle |
| SpringBoot| Broadcom |
| Maven | Apache Software Foundation |
| Typescript | Microsoft |
| NestJS | Kamil Mysliwiec |
| Npm | Npm Inc |
| Prometheus | Cloud Native Computing Foundation (CNCF)|
| Grafana | Grafana Labs |
| Swagger | SmartBear Software |
| RabbitMQ | Broadcom |
|PostgresSQL | The PostgreSQL Global Development Group |


## Funcionamento da Integração:

Uma vez que o usuário efetue algum processo relacionado à Contábil , Fiscal, Jurídico e RH no ERP Nacional , o ERP deverá efetuar uma requisição para o EndPoint REST de Autenticação do Integrador passando User e Senha,
ao qual será validado na base Postgres (previamente cadastrado), a requisição devolverá um token JWT (Validade de 6 Horas) ao qual deverá ser utilizado pelo ERP para efetuar outra requisição ao EndPoint REST (Post , trafegando JSON(contendo informações de negocio) e utilizando Https).  

Ao Receber a requisição o Nginx deverá verificar o Producer que se encontra disponivel e deverá distribuir o JSON ao mesmo.

O Producer deverá validar e posteriormente converter o JSON para o Padrao de Mensageria ao qual o Broker RabbitMQ espera (Exchange/Queue) e postar o Mesmo na sua respectiva Exchange/Queue

Os Consumers deveráo estar monitorando as Exchanges/Queues , sendo assim o que estiver livre deverá pegar a mensagem convertida(XML) e inserir na respectiva tabela do postgres com o status Ready for shipment,
após efetuar o insert only com sucesso deverá retornar http code 200 ao Nginx que fará o retorno a sua respectiva origem, em caso de erro deverá retornar 400 .

O RabbitMQ vai utilizar Persistent Volume no EKS , basicamente serve para manter os dados mesmo após o pod ser reiniciado, recriado ou movido para outro nó. 

O RabbitMQ deverá possuir Dead Letter Exchange configurada enviando após 3 tentativas falhas para DLQ Consumer

RabbitMQ Queue → Consumer (3 tentativas) → Dead Letter Exchange → DLQ Consumer (alerta humano)

uma Cron Job Adaptativo com Controle de Timeout que executa de 5 em 5 minutos deverá varrer as tabelas e obter os registros com ready for shipment efetuando o envio para o SAP ECC (Autenticação Basic Usuário e Senha) em lotes , atualizando todos que tiveram sucesso para o status processed

 O Cron Job adaptativo ajusta dinamicamente o tamanho dos lotes com base no tempo real de resposta do SAP ECC, o sistema deverá monitorar continuamente o tempo de resposta do SAP ECC, lotes menores serão enviados automaticamente quando o SAP estiver lento,
 lotes maiores quando a performance estiver ok.

Logica: 

Monitora continuamente o tempo de resposta do SAP ECC

Tempo limite por lote: 50 segundos (margem de 10s dos 60s totais)

Tamanho do lote varia de 2 a 8 registros conforme performance:

* SAP rápido (< 3s): lote de 8 registros
* SAP normal (3-6s): lote de 5 registros
* SAP lento (6-10s): lote de 3 registros
* SAP crítico (>10s): lote de 2 registros

Registros não processados permanecem com status ready for shipment

No Próximo ciclo deve processar os remanescentes

Se tempo restante for inferior a 10 segundos, interrompe o lote

Todos os WebServices / APIs deverão suportar paginação

Cada Requisição possuirá 60s até apresentar time out , existe um limite de 8 mega de trafego por requisição 

## Desenho KS namespace Integrador

<img width="2012" height="759" alt="image" src="https://github.com/user-attachments/assets/6edf2707-7226-4f5f-9a8c-c095794888c7" />




## Desenho EKS namespace Observability

<img width="894" height="500" alt="image" src="https://github.com/user-attachments/assets/6acb1232-ad40-401c-a2a3-952dc8041032" />  




## Desenho Arquitetural:

<img width="2030" height="786" alt="image" src="https://github.com/user-attachments/assets/3eb9b34c-bf1c-4c06-9825-fc9bdbf63924" />



## Escopo / Pré Requisitos
Integrar SAP ECC com ERP Nacional  

Desenvolver Integrador  

Utilizar Integrador Desenvolvido para viabilizar a integracao  

Fornecimento do Usuário / Senha dos WebServices SAP ECC  

WebServices SAP ECC Acessíveis ao Integrador  

APIS ERP Nacional Acessíveis ao Integrador  

Acesso a AWS  


## Não Escopo
Configuração do SAP ECC  

Configuração do ERP Nacional

Configuração das Credenciais SAP ECC

Configuração das Credenciais ERP Nacional  

Itens não detalhados nesta solução  

Configuração de VPN

Configuracao de mTLS

Configuração Business Intelligence

Configuração do Active Directory

Gestão Manual do EKS

Não será efetuado acesso direto a Base do SAP ECC

Não será efetuado acesso direto a Base do ERP Nacional
 

## Pipeline 

Automatizar o ciclo de vida do integrador, desde a validação de código até a implantação nos ambientes AWS.

A Ferramenta base será o GitLab CI/CD 

### Fluxo Conceitual

**Etapas:**  
`[Commit]` → `[Lint]` → `[Testes]` → `[Build]` → `[Deploy Dev]` → `[Teste Contrato]` → `[Deploy Prod]`

**Responsabilidades:**  
`Developer` ↑ `Qualidade Código` ↑ `Validação Funcional` ↑ `Imagem Docker` ↑ `Homologação Automático` ↑ `Validação API (SDD)` ↑ `Produção Manual`


### Triggers (Gatilhos)

| Evento | Ação | Ambiente Destino |
|--------|------|------------------|
| Push na branch `develop` | Pipeline completa até Deploy DEV | Desenvolvimento |
| Push na branch `main` | Pipeline até Deploy PROD (manual) | Produção |
| Merge Request para `main` | Pipeline até Testes | N/A (apenas validação) |
| Tags (v1.0.0) | Pipeline completa + rollback preparado | Produção |

#### ESTÁGIOS DA PIPELINE (DETALHADO)

#### Estágio 1 - Lint (Análise Estática de Código)

Objetivo: Garantir padronização do código e identificar problemas antes dos testes.

Atividades:

Execução do ruff para análise estática (Python) ou eslint (TypeScript/NestJS) ou Checkstyle + PMD (Java/Spring)

Execução do black ou prettier para formatação

Validação de segurança básica (bandit, se Python, Semgrep se Typescript, FindSecBugs se Java )

Critério de Sucesso:

0 erros de lint

0 warnings críticos de segurança

Tempo Estimado: 30 segundos

Falha na etapa: Pipeline interrompida, notificação ao autor do commit.  


#### Estágio 2 - Testes (Unitários e Integração)
Objetivo: Validar funcionalidades e integração com banco de dados.

Sub-etapas:

2.1. Testes Unitários
Cobertura mínima exigida: 80% (linhas de código)

Frameworks sugeridos: pytest (Python) ou JUnit (Java/Spring) ou Jest(Typescript)

Foco nos REST↔SOAP, regras de negócio (paginação, timeout)

2.2. Testes de Integração
Banco PostgreSQL em container (GitLab Services)

Teste de conexão simultânea com SAP ECC (mock) e ERP Nacional (mock)

Simulação de alto volume (até 350k registros/semana)

2.3. Testes de Contrato (SDD)
Validação da API do integrador contra o OpenAPI/Swagger definido pelo FrontEnd Vue.js

Uso da biblioteca schemathesis para geração automática de testes

Critério de Sucesso:

100% dos testes unitários passando

100% dos testes de integração passando

Cobertura ≥ 80%

Tempo Estimado: 3-5 minutos

Artefatos Gerados:

Relatório de cobertura (HTML)

Logs de testes (JSON)

### Estágio 3 - Build (Construção da Imagem Docker)
Objetivo: Criar imagem executável do integrador para deploy.

Atividades:

Leitura do Dockerfile (multi-stage para otimização)

Build da imagem com tag baseada no commit

Tag latest para ambiente DEV, tag stable para PROD

Push para Amazon ECR (Elastic Container Registry)

Critério de Sucesso:

Build concluído sem erros

Imagem < 500MB (otimizada)

Push para ECR confirmado

Tempo Estimado: 2-3 minutos

Artefatos Gerados:

Imagem Docker armazenada no ECR


#### 4 - Deploy (Implantação)  

4.1. Deploy em Desenvolvimento (Automático)
Objetivo: Atualizar ambiente DEV para validação interna.

Atividades:

Conexão com AWS EKS

Force new deployment do serviço integrador-dev

Health check: aguardar endpoint /health retornar 200

Critério de Sucesso:

Novo container em execução

Health check OK em até 60 segundos

Tempo Estimado: 2 minutos

Rollback automático: Se health check falhar, mantém versão anterior.

4.2. Deploy em Produção (Manual - Aprovação)
Objetivo: Implantar em PROD com validação humana.

Atividades:

Executado apenas na branch main

Requer aprovação manual no GitLab (via approvers rule)

Após aprovação, atualiza serviço integrador-prod

Executa smoke tests pós-deploy

Critério de Sucesso:

Aprovação manual obtida

Deploy concluído e validado

Tempo Estimado: 5 minutos (incluindo aprovação)

## Métricas  

### Prometheus  

No cluster EKS já existente mas em um namespace separado chamado Observability estará o Prometheus .

Sua função é a de coletar métricas de todos os Pods (POD01 a POD13), sendo FrontEnd , Nginx, RabbitMQ (filas, consumers, producers), Banco de dados (Base Integrador, replica 1 , replica 2), CronJob, Kubernetes (CPU, memória, rede, número de réplicas, restart de pods).

Se conecta das seguintes formas:

ServiceMonitor (Prometheus Operator) aponta para os endpoints /metrics de cada aplicação

RabbitMQ expõe métricas via plugin Prometheus.

Banco de dados via Postgres Exporter.

## Monitoramento

### Grafana

No cluster EKS já existente mas em um namespace separado chamado Observability estará o Grafana.  

Sua função é fonecer dashboards para visualização das métricas provenientes do Prometheus.

O que será monitorado visualmente nos dashboars:  

Por POD: uso de CPU/memória, latência de respostas HTTP (200), taxa de erro.

RabbitMQ: tamanho de filas, taxa de publish/consume, consumers ativos.

Base de dados: conexões ativas, tempo de query, taxa de inserção/leitura , taxa de replica.  



## Banco de Dados - Arquitetura Master / Réplicas

O PostgreSQL será configurado em cluster com 1 nó Master e 2 nós Réplicas (Slaves):

- **Master (POD10):** Responsável por todas as operações de escrita (INSERT dos 3 Consumers e UPDATE do Cron Job). Permite leitura apenas em cenários de contingência.

- **Slave 1 (POD11):** Dedicada exclusivamente para leitura pelo Cron Job. Isola a varredura dos lotes (a cada 5 minutos) das operações de escrita.

- **Slave 2 (POD12):** Dedicada exclusivamente para leitura pelo Front End (Vue.js). Garante que os dashboards de monitoramento não impactem a performance da ingestão de dados.

A replicação é feita via Streaming Replication do PostgreSQL, com tempo de atraso inferior a 1 segundo em condições normais.

Esta arquitetura garante que os 350 mil registros semanais sejam processados sem contenção entre operações de leitura e escrita, além de fornecer alta disponibilidade para consultas de monitoramento.  


### Política de Sanitização da Base de Dados

Será implementado um script automatizado de limpeza (housekeeping) para controle do crescimento da base de dados e conformidade com políticas de retenção de dados.

**Configuração da Política:**

| Parâmetro | Valor |
|-----------|-------|
| **Frequência** | Mensal (último dia de cada mês) |
| **Horário** | 23:00 (horário de baixa demanda) |
| **Critério de retenção** | Manter registros dos últimos 10 dias |  

Registros com status `processed` há mais de 10 dias serão eliminados.  

Registros com status `ready_for_shipment` ou `error` NÃO serão removidos (aguardam processamento).  

A limpeza é realizada apenas no Master, replicada automaticamente para os Slaves.  


## Cronograma do Projeto de Integração SAP ECC × ERP Nacional

### Visão Geral do Cronograma

**Duração Total:** 8 a 12 semanas (2 a 3 meses)

| Fase | Período | Atividades Principais | Duração |
|------|---------|----------------------|---------|
| Fase 1 | Semana 1-2 | Setup EKS + PostgreSQL Master/Slave + RabbitMQ DLQ | 2 semanas |
| Fase 2 | Semana 3-4 | Desenvolvimento Producer/Consumer (REST → SOAP) | 2 semanas |
| Fase 3 | Semana 5-6 | Cron Job adaptativo + lote dinâmico | 2 semanas |
| Fase 4 | Semana 7-8 | Monitoramento + Pipeline CI/CD + Testes | 2 semanas |
| Fase 5 | Semana 9-12 | Homologação + Ajustes + Deploy Produção | 4 semanas |




