## 📝 ANOTAÇÕES DO PROJETO: Provisionamento de Função Lambda (IaC)

### Título: Stack Lambda com Código In-line e Gerenciamento de Permissões (IAM)

Este documento contém os principais insights adquiridos durante o provisionamento de uma Função AWS Lambda, com foco na criação e ligação do recurso de segurança (Role IAM) e na inclusão do código-fonte.

---

### 1. Novo Desafio: Gerenciamento de Permissões (IAM)

A criação da Stack exigiu o provisionamento de uma **Role IAM** separadamente e a ligação dela à Função Lambda.

| Conceito | Recurso CloudFormation | Aprendizado |
| :--- | :--- | :--- |
| **Role IAM** | `AWS::IAM::Role` | Recurso que define as permissões que a Lambda pode ter, como a permissão para escrever logs no CloudWatch. |
| **Ligação de Recursos** | `!GetAtt NomeDaRole.Arn` | A Função Intrínseca `!GetAtt` foi crucial para obter o ARN (Amazon Resource Name) da Role IAM e atribuí-lo à propriedade `Role` da função Lambda, estabelecendo a conexão de segurança. |
| **Política de Confiança** | `AssumeRolePolicyDocument` | Definiu que o serviço Lambda (`lambda.amazonaws.com`) é o único que pode assumir essa Role para execução. |

### 2. Implementação do Código e Runtime

O código da função foi incluído diretamente no template.

* **Propriedade de Código:** `Code: ZipFile: |`
* **Vantagem:** O uso do código *in-line* simplifica o processo de IaC para scripts curtos, eliminando a dependência de uploads prévios de arquivos `.zip` para o S3.

---

### 📸 Evidências do Sucesso

As capturas de tela comprovam que o template provisionou a infraestrutura corretamente e que a função está operacional.

#### 1. Status da Stack Concluído (CREATE_COMPLETE)

Esta imagem demonstra que a Stack foi lançada com sucesso no CloudFormation.
*(Referência ao print: `Captura de tela 2025-11-02 070407.png`)*

![Status CREATE_COMPLETE Lambda](01_CFN_Lambda_Complete.png)

#### 2. Execução da Função Lambda e Log de Sucesso

Esta imagem comprova que a Função Lambda, com o código e a Role IAM provisionados, pode ser executada com sucesso.
*(Referência ao print: `Captura de tela 2025-11-02 071345.png`)*

![Teste de Execução da Função Lambda](02_Lambda_Code_Test.png)
