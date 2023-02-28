Apresentação Microsserviços
Antes de falarmos um pouco sobre o que são microsserviços, vamos falar o que geralmente vem antes deles, porque, é geralmente, quando começamos um produto, nós pensamos em como entregar valor mais rápido, e geralmente é, fazendo um monólito.

Monolito
- O monolito
    - O monólito, nada mais é que, um sistema único, ou uma unidade de implantação, uma unidade de deployment (quando todo o sistema deve ser deployado junto), que é o que temos hoje na wmapi, ela é um monólito.

- Tipo de monolito
- Single-process monolith
    - Todo código está em um processo só. Leem dados de um único banco de dados.​
    - Parece ser o classico monolito, mas é menos comum temos esse tipo de monólito (onde todo o código está ligado a um banco só)
- Monolito Modular
    - Processos são separados em módulos, cada um trabalhando independentemente, mas ainda são deployados juntos;​
    - Ainda é possível paralelizar o trabalho de cada módulo;​
    - Geralmente o banco de dados não é modular como o código.​
- Monolito distribuido
    - Sistema de possui múltiplos serviços (com dados separados), mas - por algum motivo ele ainda é necessário ser feito um deploy inteiro
    - Geralmente ele surge quando temos um alto grau de acoplamento na arquitetura

Desvantagens
* Dificuldade em escalar as partes críticas; (se quisermos só escalar uma parte crítica do monólito, não conseguimos)
* Implantações maiores e com maior impacto; (deploys maiores, geralmente acabam sendo mais demorados e tendo mais impacto)
* Menor robustez;
* Tecnologia homogênea. (Uso de uma única tecnologia)


Microserviço
Alguns conceitos chave que definem os microserviços são:
- Implantação independente: O deploy de cada microserviço é feito separadamente e, uma mudança feita em um microserviço não afeta os outros (e nem depende de outros). Para que consigamos deploys independentes, precisamos ter contratos sólidos e estáveis entre os serviços e nossos serviços devem ser ter o mínimo de acoplamento.
- Modelagem por domínio de negócio: uso de domínios do negócio para representar os limites dos nossos serviços, fazendo isso, é mais fácil criar novas funcionalidades e recombinar nossos serviços em diferentes formas. Um método muito usado é o domain driven design para definir esses limites.
- Responsabilidade sobre o próprio estado: Cada microserviços deve ser responsável pelos seu dados e estado. Para isso, não compartilhamos banco de dados. Caso um microserviço precisa de um dado, ele deve requisitar esse dado através do contrato estipulado. Assim, temos que saber decidir o que deve ser compartilhado e o que deve ser escondido. Conceito muito importante para a independência de implantação
- Tamanho: qual o tamanho ideal de um microserviço? É uma questão difícil de mensurar, o ideal deveria ser grande o suficiente para ser fácil de entender-lo. Mas o autor do livro fala que na criação de um microserviço, talvez não precisamos nos preocupar tanto com isso.
- Flexibilidade: Microserviços te abre um leque de possibilidades tecnológicas, mas também pode  trazer custos. E por isso, temos que ter um equilíbrio entre deixar as opções abertas e lidar com esse custo de um arquitetura mais complexa. Quanto mais fragmentado os serviços, mais  complexo e flexível eles são. Uma vantagem dos microsserviços é que podemos adotar incrementalmente para ir medindo esse equilíbrio.
- Alinhamento entre arquitetura e organização: O sistema reflete a organização e vice versa. Se os sistemas sua pequenos, os times deve ser também, isso faz com que, se há uma necessidade de funcionalidade, essa mudança afetará só um time.

- Desvantagens
    - Experiência de desenvolvimento: com um grande número de serviços, se torna inviável executar todos ao mesmo tempo em ambiente de desenvolvimento. Uma possível solução disso seria limitar o escopo do que o desenvolvedor deve mexer, mas pode acarretar em diminuir o senso de propriedade do time.
    - Sobrecarga de tecnologia: Com microserviços, vem novas tecnologias para trabalhar e isso toma tempo dos desenvolvedores para aprender sobre essas novas tecnologias.
    - Custo: O custo inicial dos microserviços acaba aumentando, pois precisa de mais processos, armazenamento, serviços, etc. E outro custo é o custo do desenvolvedor, que vai demorar mais tempo para aprender tecnologias novas, e isso irá impactar o tempo de outros entregas.
    - Relatórios:
    - Monitoramento e solução de problemas
    - Segurança
    - Testes
    - Latência
    - Consistência de dados

- Quem não deveria usar
    - Produtos novos e startups, já que o domínio de negócio é muito volátil e passível de mudanças;


————————————————————————————————————————


Tipos de monolito​

Single-Process Monolith​

Todo código está em um processo só. Leem dados de um único banco de dados.​

The Modular Monolith​

Processos são separados em módulos, cada um trabalhando independentemente, mas ainda são deployados juntos;​

Ainda é possível paralelizar o trabalho de cada módulo;​

Geralmente o banco de dados não é modular como o código.​

The Distributed Monolith​

Sistema que consiste em multiplos serviços, mas por algum motivo, deve ser feito deploy junto.​

​

Vantagens​

Simples de fazer deploy;​

Workflow de desenvolvimento pode ser mais sistemas, assim como monitoramento e testes end-to-end;​

Mais facil de reutilizar codigo dentro do monolito.​

Desvantagens​


Microserviço
Serviços com releases independente entre si que são modelados em volta de um domínio de negócio;​

Um serviço que encapsula funcionalidades e deixa-as disponíveis através de redes;​

De fora, é uma caixa preta;​

Evita DBs compartilhados;​

Tende a expor o mínimo de informação pelas interfaces externas, assim o que não está exposto, pode mudar sem problemas, contanto que a interface externa não mude (Information hiding);

Conceitos Chave

Deploy independente​

Deploy de cada microsserviço é feito separadamente e não afeta os outros microsserviços (e nem depende de outros deploy);​

Para que isso funcione, os microsserviços precisam ter pouco acoplamento (mudar um serviço não implica que eu precise fazer deploy/mudança entre outro);​

Para isso, precisamos ter contratos sólidos entre os serviços;​

​

Modelagem em volta de um modelo de negócio​

Necessidade de estruturar o código que representem um domínio do mundo real;​

Usamos Domain-Driven Design para definir os limites de cada serviço;​

Facilita criar novas funcionalidades e recombinar microsserviços em diferentes formas para entregar-las.​

​

Responsável pelo próprio estado​

Não compartilhar banco de dados. Se um microsserviço quer um dado de outro, tem que comunicar com o outro;​

Habilidade de decidir o que é compartilhado e o que é escondido de outros microsserviços;​

O microserviço tem que ser dono dos dados necessários naquele domínio.​

​

Tamanho​

Qual o tamanho de um microsserviços? O tamanho deve respeitar a facilidade de entendimento do mesmo;​

Não se preocupar tanto com o tamanho.​

Flexibilidade​

Equilíbrio entre deixar suas opções abertas e lidar com o custo de uma arquitetura mais complexa;​

Adoção incremental de microsserviços (mais fácil de entender o impacto aos poucos)​

Alinhamento de arquitetura e organização​

Organização dos times sempre refletem a organização dos sistemas/código​

Se os sistemas são pequenos serviços individuais, os times deverão ser também, assim, quando é necessário mudança em uma funcionalidade, só afetará um time só.

Vantagens​

Vantagens​

Heterogeneidade tecnológica​

Podemos escolher usar diferentes tecnologias dentro de cada microsserviço;​

Escolhemos a ferramenta certa pra cada tarefa;​

Risco é menor de testar e adotar uma nova tecnologia.​

Robustez​

Um componente pode falhar, mas se o resto está funcionando, fica mais fácil de isolar o problema e o resto do sistema, vai continuar funcionando;​

Temos que saber lidar com as falhas e o impacto delas no sistema.​

Scaling​

Com microsserviços, podemos escalar só o que precisa ser escalado.​

Facilidade no deploy​

No monolito, se mudarmos algo, todo monolito deve ser deployado. Nos microsserviços, podemos fazer uma mudança em um serviço e fazemos o deploy independente dos outros serviços. Assim, o código é deployado mais rápido, e o rollback fácil de fazer.​

Alinhamento organizacional​

Times menores com menores codebases são mais fáceis de gerir e são mais produtivos que grandes times com codebases grandes (monolitos);​

Conseguimos alinhar a arquitetura dos microsserviços com a organização.​

Composability​

Abre a possibilidade de reutilização de funcionalidades. Os microserviços podem ser consultados em diferentes maneiras pelos clientes.

Desvantagens​

Developer Experience​

Número de serviços que posso rodar local ao mesmo tempo é pequeno. A solução seria limitar o escopo de que partes o dev deve mexer, mas tira a collective ownership do time​

​

Tecnology Overload​

Microsserviços trazem novas tecnologias para se trabalhar. Deve-se tomar cuidado ao balancear o tamanho e complexidade da tecnologia que será usado contra os custos destas tecnologias;​

Leva-se tempo para aprender as tecnologias, aumentando o tempo de entrega de features novas;​

​

Custo​

O custo de inúmeros fatores irão aumentar no começo. (precisamos rodar mais processos, mais storage,...)​

Qualquer tecnologia/ideias/conceitos novos, vai demandar tempo de devs para aprender a usar tudo isso, impactando outras features.​

​

Reporting​

Nos microsserviços, temos um schema distribuídos, é mais difícil conseguir reports do sistema inteiro, já que temos que acessar vários serviços;​

Monitoramento e Troubleshooting​

Com microsserviços (com centenas de processos), é mais difícil dizer, por exemplo, se um processo só que está com CPU a 100%, se isso é um problema.​

Segurança​

Como os dados passam por várias redes entre os serviços, os dados ficam mais vulneráveis a serem observados durante este caminho;​

Precisamos assegurar a proteção nesses caminhos de dados.​

Testes​

Testes end-to-end são muito grandes e complexos (já que envolvem inúmeros serviços).​

Latência​

Os processos são divididos em múltiplos serviços. Informação que antes passava por um único processo, agora passa por vários microsserviços (precisam ser serializados, transmitidos e deserializados entre networks), fazendo com que a latência desses processos aumente.​

Consistência de dados

Para quem microsserviços pode funcionar:​

Empresas que querem que os desenvolvedores trabalhem separadamente, mas no mesmo sistema;​

SaaS;​

Para quem quer distribuir um sistema em vários "canais" diferentes;​

Microsserviços trazem muita flexibilidade de evolução de um sistema.​

​

Para quem os microsserviços pode não funcionar:​

Produtos novos e startups, já que o domínio de negócio ainda vai mudar muito enquanto estiver sendo construído. Startups geralmente tem poucas pessoas construindo o sistema.​

Organizações que o deploy e gestão é feita pelos clientes. Fica mais difícil de trabalhar se o seu cliente precisa "baixar" vários pedaços do sistema.
