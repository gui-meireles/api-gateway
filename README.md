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

---

## Kong API Gateway

O Kong atua como um intermediário entre clientes e serviços, fornecendo recursos como autenticação, autorização, monitoramento,
limitação de taxa, transformação de dados, entre outros.

No site: https://docs.konghq.com/hub/ podemos adicionar plugins ao nosso Kong para nos ajudar a configurar o API Gateway.

### Subindo o Kong

Caso a imagem `claudioed/kong-fc` no arquivo `kong_compose.yml` não funcione, você pode criar uma imagem e subir ela utilizando o
exemplo em `/docker/Dockerfile`.

> **O que é o Konga ?**
> 
> Interface administrativa para o Kong API Gateway;
> 
> Visualização de métricas das instâncias;
> 
> Controle de usuários.
> 
> Site: https://github.com/pantsel/konga

**Subindo o docker-compose:**

Com o seu terminal aberto na pasta `./compose`, rode o comando: `docker-compose -f kong_compose.yml up`.

Ao carregar todos os containers, acesse seu navegador: `localhost:8085`, será aberto a tela do Konga.

- Crie um login para ter acesso ao portal.

### Configurando as Services

A função **services** é utilizada para configurar e gerenciar os serviços que serão expostos através do API Gateway Kong.

Esses serviços representam as aplicações ou microserviços que serão acessados pelos clientes através da API.

**Vamos configurar o microserviço de bets do `kong_compose.yml` no Konga**

Na interface do Konga, cadastre um novo serviço:
![img.png](readme_images/service.png)

### Configurando as Rotas

É o "caminho" de url que permitirá que um serviço seja acessado pelo Kong API Gateway.

**Vamos configurar a rota no Konga**

Na interface do Konga, clique no serviço que foi criado acima e clique em `Routes`:
![img.png](img.png)
![img_1.png](img_1.png)

Após essas configurações, clique em `Submit Route`.

> No `kong_compose.yml`, temos o container do Kong e fazemos um forward da porta 8000 do proxy para a porta 80 da nossa máquina.
![img_2.png](img_2.png)

Com isso, conseguimos acessar o serviço de `bets` e criar uma aposta pelo **Postman**:

![img_3.png](img_3.png)

E no Body, selecione a opção `raw`, `JSON` e cole o código abaixo:

`{
"match": "1X-DC",
"email": "joe@joe.com",
"championship": "UEFA Champions League",
"awayTeamScore": "2",
"homeTeamScore": "3"
}`

>E ao enviar, você deverá receber uma mensagem semelhante a:
![img_4.png](readme_images/img_4.png)
![img_4.png](img_4.png)

## Configurando Plugins

Os plugins no Kong são funcionalidades adicionais que podem ser adicionadas ao API Gateway para estender suas capacidades,
podem ser configurados nas Rotas, Serviços, Consumers e Globalmente.

> Alguns exemplos de plugins incluem autenticação, autorização, transformação de dados, rate limiting, logging, entre outros.

E você pode escreve-los usando a linguagem **lua, javascript e golang** ou utilizar os que já existem na comunidade.

### Configurando o plugin `Correlation ID`

Para isso, vamos utilizar o plugin `Correlation ID`, que gera um ID único para cada solicitação e o inclui nos cabeçalhos
das requisições: https://docs.konghq.com/hub/kong-inc/correlation-id/

- Na interface do Konga, vamos abrir a aba de `Plugins`:
![img_5.png](img_5.png)

- Configure e adicione o `Correlation ID`:
![img_6.png](img_6.png)

E ao enviar uma nova request pelo `postman`, podemos ver que foi adicionado um **novo parametro** no Header da response:
![img_7.png](img_7.png)

