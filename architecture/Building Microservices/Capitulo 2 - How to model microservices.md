Capitulo 2 - How to model microservices

Microsserviços - composição modular de serviços com interações baseadas em redes.

What Makes a Good Microservice Boundary?
- Information Hiding: desejo de esconder o máximo detalhes possíveis atrás de um limite modulo (ou microsserviço)
   - Benefícios:
     - Tempo de deploy melhorado: modulos são desenvolvidos separadamente, assim mais trabalho é feito em paralelo.
     - Compreensibilidade: cada módulo pode ser olhado isoladamente e compreendido isoladamente. Sendo mais fácil entender o sistema como um todo.
     - Flexibilidade: modulso podem mudar independente de outros, assim um módulo pode mudar sem afetar os outros.
     - Assumption: o que conecta dois módulos diminuindo a quantidade de assumptions é mais fácil garantir que uma mudança no módulo não vai afetar outros.

Coesão
- Comportamentos parecidos ficam juntos, para que, se algo mudar, mudamos em um lugar só para ser fácil, rápido e barato deployar uma feature, por exemplo.

Coupling
- Baixo acoplamento é quando uma mudança afeta o mínimo de serviços possíveis. Ex: um deploy só afeta um serviço. Serviços desacoplados sabem o mínimo de outros serviços colabora.

Relação entre coesão e acoplamento.
- Sistemas estáveis tem coesão alta e acoplamento baixo.
- Coesão fala sobre limite dentro de um microserviço.
- Acoplamento limite entre microserviços temos que achar o equilíbrio entre esses dois conceitos.

Tipos de acoplamento
- Nem todo acoplamento é ruim
- Domain Coupling:
    - Um microserviço interage com outro, porque ele precisa usar uma funcionalidade do outro.
    - Impossível evitar, mas deixar mínimo.
    - Um microsserviço que fala com muitos outros pode indicar que muita lógica esta centralizada.
    - Pode ser problemático se muitos dados complexos estão sendo passados de um para outros.
    - Temporal coupling: conceitos estão juntos só porque eles acontecem no mesmo tempo. Em microsserviços é quando um microserviçø precisa de uma informação de outro para terminar uma ação.

- Pass-through Coupling
    - Um microsserviço passa dados para outro porque esses dado é necessário em outro ponto do sistema. Muito perigoso.
    - Não só o "chamados" conhece essse dado, mas algum microsserviços lá na frente conhece também.
    - Uma mudança no dado lá no downstream afeta o upstream.
    - Como resolver: entender se precisa ter esse serviço mediados para passar o dado separando os dados que serão repassados para serviços diferentes.

- Common coupling
    - 2 ou mais microsserviços usam o mesmo dado. Ex: 2 microsserviços usando o mesmo banco de dados, mesma memória ou mesmo filesystem.
    - Se o schema do banco de dados mudar, todos os serviços são afetados.
    - Solução do livro: um serviço controla a mudança de estado.
    - Se um serviço parece só tem um CRUD simples com um DB, pode ser que alguma lógica que deveria estar ali está em outro lugar.
    - Common coupling pode trazer overload onde estiver o compartilhamento.

- Content Coupling
    - Um serviço upstream muda o estado interno de um serviço downstream.
    - Ex: um serviço externo mudando e acessando um DB de outro serviço diretamente, quando isso acontece o DB se trona parte do contrato externo. A habilidade de dizer o que é compartilhado e o que é escondido foi perdida.

Domain Driven-design
    - Design de sistemas que definem o mundo real.
Conceitos:
- Uniquitous Language: usar os mesmo termos que são usados na vida real no código. Melhora a comunicação entre times.
- Aggregate: coleção de objetos geridos por uma entidade. Unidade auto contidas. Algo que tem estado, identidade, lifecycle gerido dentro do sistema que refleta conceitos reais.
- Bounded Context: Um limite de negócio que prove uma funcionalidade para um sistema. Esconder detalhes de implementação.
Modelos:
- Hidden Models: um serviço não precisa saber como funciona o funcionamento interno, mas precisa saber o mínimo. Separe-os.
- Shared Models: conceitos podem estar em mais de um bounded context

Aggregate e bound context nos microserviços
- No começo faça serviços que englobe um bound context inteiro e depois quebre em menores e lembre que um aggregate está em um microsserviço só.
- Possível quebra dentro de um microsserviços em serviços menores para os serviços externos ainda será um só.

Event Storming
- Brain storming para montar um modelo de domínio. Pessoas técnicas e de negócio
    - Primeiro identificar eventos de domínios.
    - Segundo identificar o que chama cada evento.
    - Terceiro entendner o que faz parte do que.
    - Agrupar em bounded context.

Resumo de DDD para microserviços
- Esconder informação - limite claro entre partes do sistema escondendo a complexidade interna.
- Mesmo termos de negócio para técnico, bom para definir endpoints.