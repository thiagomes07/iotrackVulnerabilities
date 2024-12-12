# Relatório de Vulnerabilidades e Pontos de Ataque

Realizamos uma análise detalhada do projeto de mapeamento de ativos com o objetivo de identificar vulnerabilidades e possíveis ataques. Identificamos quatro itens principais que comprometem a segurança do sistema.

## 1. Tabela Consolidada de Ataques

<div align="center">

| **Título do Ataque ou Vulnerabilidade**         | **Nível de Impacto** | **Nível de Risco** |
|--------------------------------------------------|----------------------|--------------------|
| **Tokens Reutilizáveis**                         | Alto                 | Alto               |
| **Brute Force no Login**                         | Alto                 | Alto               |
| **Tags RFID Vulneráveis**                        | Médio                | Médio              |
| **Acesso ao Código via Decompilação do ESP32**   | Baixo                | Baixo              |

</div>

### Detalhamento

1. **Tokens Reutilizáveis** (Vulnerabilidade)
   - **Descrição**: A ausência de uma *blacklist* para tokens *JWT* permite que um mesmo *token* seja reutilizado em múltiplos dispositivos. Além disso, o sistema não implementa mecanismos para invalidação de sessões já autenticadas, tornando as credenciais válidas mesmo após situações críticas, como alterações de senha.
   - **Impacto**: *Alto*. Essa vulnerabilidade expõe dados sensíveis a terceiros não autorizados, aumentando significativamente o risco de vazamento de informações.
   - **Risco**: *Alto*. Devido à sua natureza sistêmica, é prioritário mitigar essa vulnerabilidade com soluções como *blacklists*, redução no tempo de validade dos tokens e autenticação reforçada.

2. **Brute Force no Login** (Possível Ataque)
   - **Descrição**: O sistema não limita o número de tentativas consecutivas de *login*. Isso permite ataques de força bruta (*brute force*), onde um atacante tenta diversas combinações de usuário e senha de forma automatizada. Não há implementação de bloqueios temporários ou *captchas* que possam mitigar essas tentativas.
   - **Impacto**: *Alto*. Um ataque bem-sucedido comprometerá as credenciais do usuário, permitindo acesso irrestrito ao sistema.
   - **Risco**: *Alto*. A facilidade em executar este tipo de ataque exige medidas preventivas como autenticação multifator (*MFA*) e limitação de tentativas por intervalo de tempo.

3. **Tags RFID Vulneráveis** (Vulnerabilidade)
   - **Descrição**: As *tags* RFID utilizadas no sistema carecem de medidas básicas de segurança, como criptografia dos dados armazenados. Além disso, elas permitem sobrescrição de *IDs* sem validação, possibilitando que atacantes com acesso físico reescrevam ou clonem informações.
   - **Impacto**: *Médio*. Apesar de exigir acesso físico ao dispositivo, a ausência de segurança nessas *tags* permite manipulação maliciosa de dados, impactando a integridade do sistema.
   - **Risco**: *Médio*. A vulnerabilidade pode ser explorada com equipamentos simples e conhecimento básico de RFID. Recomenda-se a adoção de criptografia e autenticação robusta nas *tags*.

4. **Acesso ao Código via Decompilação do ESP32** (Vulnerabilidade)
   - **Descrição**: O firmware do dispositivo ESP32 pode ser extraído por meio de engenharia reversa. O código fonte acessado desta forma pode expor informações sensíveis, como chaves de acesso, ou permitir ataques mais sofisticados baseados no entendimento da lógica interna do sistema.
   - **Impacto**: *Baixo*. Embora a engenharia reversa do código possa oferecer insights valiosos para um atacante, seu impacto geral é limitado devido à necessidade de acesso físico e ferramentas avançadas.
   - **Risco**: *Baixo*. A complexidade e os recursos técnicos necessários reduzem a probabilidade de exploração. Sugere-se a aplicação de técnicas de ofuscação e proteção contra leitura de memória.

## 2. Contribuições dos Membros do Grupo

### Paulo
- Análise, apresentação ao ateliê e levantamento das vulnerabilidades relacionadas aos *tokens JWT*.

### Leonardo
- Identificação e detalhamento do possível ataque de *brute force* no *login*.

### Iasmin
- Pesquisa, apresentação ao ateliê e documentação sobre as vulnerabilidades das tags RFID.

### Thiago
- Avaliação das vulnerabilidades do código fonte do ESP32, documentação em *markdown* e riscos associados.

### Gabriela
- Consolidação da tabela, *slides* para a apresentação e classificação de impacto e risco.

### Gabriel
- Revisão final, levantamento de riscos e distinção dos riscos entre vulnerabilidade e pontos de ataque.
