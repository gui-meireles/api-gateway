# Api Gateway

### O que são APIs ?

Uma API (Interface de Programação de Aplicativos) é um conjunto de regras e definições que permite
que diferentes softwares se comuniquem entre si.

Em termos simples, uma API permite que um software utilize os recursos de outro software de forma controlada e segura.


### O que é Gateway ?

O API Gateway é um padrão de projeto que atua como um intermediário entre clientes e serviços back-end.

Ele ajuda a simplificar a arquitetura de microserviços, melhorar a segurança, facilitar a manutenção e gerenciar o tráfego de rede.

Em resumo, o API Gateway funciona como uma porta de entrada para as APIs, simplificando o acesso e a gestão das mesmas.

### Algumas Funcionalidades

- **Roteamento de requisições:** direcionar as requisições dos clientes para os serviços apropriados.

- **Autenticação e autorização:** garantir que apenas usuários autorizados tenham acesso aos serviços.

- **Monitoramento e análise de tráfego:** coletar métricas e dados de uso das APIs.

- **Transformação de dados:** converter formatos de dados, como JSON para XML, por exemplo.

- **Cache de respostas:** armazenar em cache respostas para reduzir o tempo de resposta.

- **Rate limiting:** controlar a taxa de requisições para evitar sobrecarga nos serviços.

- **Logging e rastreamento:** registrar informações para facilitar a depuração e auditoria.

- **Gerenciamento de versões:** suportar múltiplas versões de APIs e controlar sua evolução.

### Vantagens e Desvantagens

**Vantagens:**

- Padronização de segurança e logging;
- Ajuda na governança de rede;
- Ponto único de entrada na rede, facilitando o gerenciamento.

**Desvantagens:**

- Adiciona complexidade na arquitetura;
- Precisa de um cuidado extra, devido a disponibilidade **(ter no mínimo 3 instâncias)**;
- É uma ferramenta que precisa de manutenção/atualização devido as vulnerabilidades.
