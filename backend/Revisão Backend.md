# Revisão Backend

## Circuit Breakers

Como impedir que erros/falhas de um microserviço cascateiem para outros serviços que invocaram o primeiro sincronamente? Recursos importantes podem ser consumidos no microserviço chamador enquanto espera o outro responder.
Um client deve invocar um serviço remoto via proxy que funciona como um circuit breaker elétrico (disjuntor).
Quando o número de falhas consecutivas ultrapassa um limite, o circuit breaker "liga" e pela duração de um periodo de timeout, todas as tentativas de invocar o serviço remoto vão falhar imediatamente. Depois que o timeout expirar, o circuit breaker permite que um número limitado de requests passem para o serviço. Se esses requests forem sucesso, o circuit breaker voltar
a funcionar, se não o periodo de timeout começa de novo.

Prós
- Serviços lidam com a falha dos serviços que eles invocam.

Contra
- É difícil escolher valores de timeout sem criar falsos positivos ou introduzir lantência excessiva.


<br>
<hr>
<br>

## Twelve-factor App

1. Codebase
    - O App está sempre versionado usando um app de versionamento (Git) e são feitos muitos deploys.
    - Um codebase por app, mas terá muitos deploys dessa app (em vários ambientes: produção, staging, local...), compartilhando o codebase.

2. Dependencies
    - Depências isoladas e declaradas explicitamente.
    - Uso de um sistema de pacotes (como package.json, gemfile) para declarar as depências explicitamente.
    - Simplifica setup para novos desenvolvedores da app.

3. Config
    - Guardar configurações como variáveis de ambiente. É o que pode mudar de um ambiente pra outro.
    - Credenciais externos, de acesso a banco, etc.

4. Backing services
    - Um backing service é qualquer serviço que a app consome por uma rede para operar normalmente (DB, AmazonS3, New Relic, etc)
    - Tratar backing services como recursos anexados, o que indica baixo acoplamento ao deploy que ele esta "anexado".
    - Assim, quando um recurso anexado da problema (um db cai, por exemplo), é fácil de trocar sem precisar mexer no código.

5. Build, release, run
    - Separa build dos estagios de run.
    - Estágio de build é quando transformamos o código num bundle executável, conhecido como build.
    - Estágio de release pega o build e combina com as configurações do deploy. A release contém o build e as configs e está pronto pra execução no ambiente.
    - Está de rum (runtime) roda a app no ambiente de execução.

6. Processes
    - A app é executada no ambiente de execução como um ou mais processos.
    - Os processos são stateless. Qualquer dado que precisa ser persistido deve ser guardado num backing service, como um DB.
    - Um twelve-factor app nunca assume que algo que está cacheado em memória ou em disco vai estar disponível num futuro request ou job. Mesmo rodando um processo só, o restart vai apagar todo estado local.

7. Port binding
    - Exportar serviços via port binding
    -  The web app  exporta HTTP as a service se vinculando a uma porta e escutando os requests vindo daquela porta.
    - Localmente geralmente a url do serviço fica: http://localhost:5000/.
    - Isso faz com que a app possa ser um backing service de outra app.

8. Concurrency
    - Processos na aplicação doze-fatores utilizam fortes sugestões do modelo de processos UNIX para execução de serviços daemon, o desenvolvedor pode arquitetar a aplicação dele para lidar com diversas cargas de trabalho, atribuindo a cada tipo de trabalho a um tipo de processo.
    - Solicitações HTTP podem ser manipuladas para um processo web, e tarefas background de longa duração podem ser manipuladas por um processo worker.

9. Disposability
    - Os processos da app são descartáveis, podem iniciar e parar a qualquer momento.
    - Processes devem se esforçar para miniminar o startup time.
    - Processos devem finalizar graciosamente quando recebem um sinal do process manager.


10. Dev/prod parity
    - Deixar development, staging e produção o mais similar possível.

11. Logs
    - Logs são tratados como stream de eventos.
    - Os logs não são escritos em um file e sim, cada processo escreve seus logs num event stream (stdout)
    - Em staging e production esses logs são juntados e colocados num local que seja fácil visualização futuras (tipo kibana, log do GCP, etc.)

12. Admin processes
    - Rode tarefas de administração/gestão em processos pontuais (Executar migrações de base de dados, executar o shell, executar scripts)
    - Processos administrativos pontuais devem ser executados em um ambiente idêntico, como os processos regulares de longa execução da app. Eles rodam uma versão, usando a mesma base de código e configuração como qualquer processo executado com essa versão.

<br>
<hr>
<br>

## Cache control

- HTTP header usado para especificr políticas de cache nas requisições do cliente e nas responses do servidor.

 - Cache-Control: Max-Age
    - Define em segundos quanto tempo demora para um dado cacheado expirar (cliente deve pedir para o servidor o dado)

 - Cache-Control: No-Cache
    - O browser pode cachear a response, mas primeiro precisa submeter um request de validação para o servidor.

 - Cache-Control: No-Store
    - Response não deve ser cacheado

 - Cache-Control: Public
    - Response pode ser cacheado por qualquer cache

 - Cache-Control: Private
    - Response só pode ser cacheado no device do client. (Por exemplo, um site pode ser cacheado pelo browser, mas não por uma CDN)
