# Relatório de Vulnerabilidades e Pontos de Ataque

Realizamos uma análise detalhada do projeto de mapeamento de ativos com o objetivo de identificar vulnerabilidades e possíveis ataques. Identificamos quatro itens principais que comprometem a segurança do sistema.

## 1. Tabela Consolidada de Ataques

| **Título do Ataque**                             | **Nível de Impacto** | **Nível de Risco** |
|--------------------------------------------------|------------------------|----------------------|
| **Tokens Reutilizáveis**                          | Alto                   | Alto                 |
| **Brute Force no Login**                         | Alto                   | Alto                 |
| **Tags RFID Vulneráveis**                        | Médio                 | Médio               |
| **Acesso ao Código via Decompilação do ESP32**  | Baixo                  | Baixo                |

### Detalhamento dos Ataques

1. **Tokens Reutilizáveis**
   - **Descrição**: Falta de *blacklist* de tokens JWT permite que o mesmo *token* seja utilizado em múltiplos dispositivos, comprometendo a segurança de sessões.
   - **Impacto**: Alto. A reutilização de *tokens* pode comprometer dados sensíveis de forma significativa.
   - **Risco**: Alto. A falta de proteção direta torna esse um ponto de ataque prioritário.

2. **Brute Force no Login**
   - **Descrição**: Não há limite de tentativas de login, permitindo ataques de força bruta para descobrir credenciais.
   - **Impacto**: Alto. Pode comprometer o acesso ao sistema.
   - **Risco**: Alto. A ausência de mecanismos de bloqueio aumenta a probabilidade de ocorrência.

3. **Tags RFID Vulneráveis**
   - **Descrição**: Tags não possuem proteção contra sobrescrição de IDs, além de não serem criptografadas.
   - **Impacto**: Médio. Permite que atacantes manipulem ou sobrescrevam informações.
   - **Risco**: Médio. Embora a exploração exija acesso físico, a vulnerabilidade é relevante.

4. **Acesso ao Código via Decompilação do ESP32**
   - **Descrição**: Possibilidade de acessar o código fonte do ESP32 por meio de engenharia reversa.
   - **Impacto**: Baixo. O impacto na segurança do sistema geral é limitado.
   - **Risco**: Baixo. Esse ataque requer conhecimentos técnicos e acesso físico ao dispositivo.

## 2. Contribuições dos Membros do Grupo

### Paulo
- Análise e levantamento das vulnerabilidades relacionadas aos tokens JWT.

### Leonardo
- Identificação e detalhamento do ataque de brute force no login.

### Iasmin
- Pesquisa e documentação sobre as vulnerabilidades das tags RFID.

### Thiago
- Avaliação das vulnerabilidades do código fonte do ESP32 e riscos associados.

### Gabriela
- Consolidação da tabela e classificação de impacto e risco.

### Gabriel
- Revisão final e organização do documento em markdown.