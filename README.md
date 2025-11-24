# Trabalho Prático: O Problema dos Leitores e Escritores

<sub>Última atualização: 21/11/2025</sub>

## Sumário

- [Objetivo](#objetivo)
- [Introdução](#introdução)
- [Tarefas](#tarefas)
  - [Implementação](#implementação)
  - [Relato](#relato)
- [Autoria e política de colaboração](#autoria-e-política-de-colaboração)
- [Entrega](#entrega)
- [Avaliação](#avaliação)
- [Dúvidas e informações](#dúvidas-e-informações)

## Objetivo

O objetivo deste trabalho é estimular o projeto e a implementação de soluções para problemas por meio de programação concorrente, mais especificamente colocando em prática os conceitos e mecanismos de sincronização de processos/*threads*.

## Introdução

O Problema dos Leitores e Escritores (*Readers-Writers Problem*) é um problema clássico no contexto de programas concorrentes, que serve inclusive como modelo para outros problemas com características similares. Proposto originalmente por P. J. Courtois, F. Heymans e D. L. Parnas em seu artigo [*Concurrent control with "readers" and "writers"*](https://doi.org/10.1145/362759.362813), publicado em 1971, o problema diz respeito à existência de um recurso compartilhado entre dois tipos de processos (leitores e escritores) que tentam acessá-lo simultaneamente. Os processos leitores realizam operações de leitura sobre o recurso compartilhado, enquanto os processos escritores realizam operações de escrita. O problema consiste, portanto, em estabelecer uma forma de sincronização entre esses processos de modo a preservar um estado consistente do recurso compartilhado.

## Tarefas

A tarefa central a ser realizada neste trabalho consiste em projetar e implementar soluções concorrentes para duas variações do Problema dos Leitores e Escritores utilizando conceitos e técnicas de programação concorrente, incluindo a criação, execução e sincronização de *threads*. Tais variações são descritas a seguir.

**Preferência aos leitores**

Considerando que o objetivo principal do Problema dos Leitores e Escritores é manter o recurso compartilhado em um estado consistente, uma solução natural ao problema seria garantir a exclusão mútua do processo que está acessando o recurso, de modo que nenhum processo poderia acessá-lo enquanto outro processo, independentemente do seu tipo, estivesse de posse dele. Todavia, essa solução, apesar de resolver o problema de forma satisfatória, não é ótima, pois os processos leitores não modificam o estado do recurso e, portanto, não precisam estar em exclusão mútua entre si.

A solução que dá preferência aos leitores (*readers-preference*) permite que um processo leitor realize uma operação de leitura sobre o recurso compartilhado, mesmo que esteja de posse de outro processo leitor. Nesse caso, se um processo escritor tentar acessar o recurso, este será bloqueado e poderá ter acesso ao recurso quando não houver mais nenhum processo leitor fazendo uso dele. Caso o recurso esteja inicialmente de posse de um processo escritor, quaisquer outros processos que desejarem acessá-lo, sejam leitores ou escritores, serão bloqueados e deverão aguardar sua liberação.

**Preferência aos escritores**

A solução que dá preferência aos escritores (*writers-preference*) prioriza a execução desse tipo de processo. Ou seja, havendo um processo escritor pronto para acessar o recurso compartilhado, a posse deste lhe será concedida, devendo quaisquer outros processos (leitores e/ou escritores) serem bloqueados em razão da exclusão mútua garantida à operação de escrita. Ao término da operação de escrita corrente, caso haja um processo escritor bloqueado, a posse do recurso compartilhado lhe será garantida. Com isso, processos leitores só poderão acessar o recurso compartilhado caso não haja nenhum processo escritor acessando ou aguardando o acesso ao recurso.

### Implementação

As soluções poderão ser implementadas utilizando facilidades das linguagens de programação C/C++, Java ou Python, sendo que outra linguagem, diferente dessas três, poderá ainda ser utilizada, contanto que a proposta seja previamente validada com o docente. O mecanismo de sincronização é de livre escolha dentre os disponibilizados pelas linguagens de programação escolhidas.

Além da implementação do núcleo de cada solução, deverá ser implementado, para fins de demonstração, um código-fonte principal que instancie um determinado número de *threads* para realizar operações de leitura e escrita sobre alguma variável, objeto ou arquivo (recurso compartilhado). A execução do programa deverá exibir, na saída padrão, o comportamento das *threads* no tocante ao acesso ao recurso compartilhado e eventuais bloqueios caso o recurso compartilhado esteja em uso.

*Dica:* Caso seja implementado um projeto único envolvendo as duas soluções, uma sugestão é solicitar ao usuário, a partir da entrada padrão, qual solução será executada, se dá preferência aos leitores ou aos escritores.

### Relato

Uma vez realizadas as tarefas de implementação, deverá ser elaborado um relatório contendo, pelo menos, uma descrição acerca:

- de como a solução foi projetada;
- a lógica de sincronização utilizada, em termos dos mecanismos empregados e como ela é feita entre os fluxos de execução do programa, além de ser justificada a escolha do mecanismo de sincronização;
- como é garantida a corretude da solução com relação a concorrência;
- eventuais dificuldades encontradas durante o desenvolvimento, e;
- instruções para a compilação e a execução do programa.

## Autoria e política de colaboração

Este trabalho deverá ser realizado em equipe composta por até dois estudantes, sendo importante, dentro do possível, dividir as tarefas igualmente entre os integrantes da equipe. Após a implementação das soluções para os problemas propostos, o arquivo [`author.md`](https://github.com/ufrn-concprog/readers-writers/tree/master/author.md) presente no repositório deverá ser editado, preenchendo as informações de identificação dos integrantes da equipe na seção [Informações de Autoria](https://github.com/ufrn-concprog/readers-writer/tree/master/author.md#identificação-de-autoria).

O trabalho em cooperação entre estudantes da turma é estimulado, sendo admissível a discussão de ideias e de estratégias. Contudo, tal interação não deve ser entendida como permissão para utilização de (parte de) código-fonte de colegas, o que pode caracterizar situação de plágio. **Trabalhos copiados, no todo ou em parte, de outros colegas ou da Internet, ou ainda gerados por ferramentas de Inteligência Artificial serão anulados e receberão nota zero.**

## Entrega

O sistema de controle de versões [Git](https://git-scm.com) e o serviço de hospedagem de repositórios [GitHub](https://github.com) serão utilizados para possibilitar a entrega da implementação. Para possibilitar a associação de repositórios do Git a cada equipe e reuni-los sob uma mesma infraestrutura, foi criada uma atividade (*assignment*) no GitHub Classroom. Cada integrante da equipe deverá acessar este [*link*](https://classroom.github.com/a/yUDknnfd), aceitar o convite para ingressar no GitHub Classroom e, em seguida, seguir as instruções em tela para acessar a atividade e ingressar em uma equipe existente ou criar outra. Este [vídeo](https://youtu.be/ObaFRGp_Eko) demonstra como ocorre esse processo.

No momento da criação de uma equipe, o GitHub Classroom cria um repositório Git privado, acessível apenas aos integrantes da equipe e ao docente, sob a organização [`ufrn-concprog`](https://github.com/ufrn-concprog). A fim de garantir a boa manutenção do repositório, deve-se ainda configurar corretamente o arquivo `.gitignore` para desconsiderar arquivos que não devam ser versionados, a exemplo dos arquivos executáveis gerados a partir da compilação do código-fonte.

A entrega deste trabalho deverá ser realizada até as **23:59 do dia 3 de dezembro de 2025** no respectivo repositório Git da equipe. O relatório elaborado, preferencialmente em formato *Adobe Portable Format* (PDF), deverá ser enviado como arquivo através da opção *Tarefas* da Turma Virtual do SIGAA, juntamente com, no campo *Comentários*, o endereço do repositório. Um único membro da equipe deve realizar esse envio e não serão aceitos envios por outros meios ou repositórios que não sejam os descritos nesta especificação.

## Avaliação

A avaliação do trabalho contabilizará nota máxima de 10,0 pontos na 2ª Unidade da disciplina. O trabalho será avaliado de acordo com os seguintes critérios:

- utilização correta dos conceitos e mecanismos de sincronização de processos/*threads*;
- a corretude da execução do programa implementado, tanto com relação a funcionalidades quanto à concorrência;
- a aplicação de boas práticas de programação, incluindo legibilidade, organização e documentação de código-fonte;
- correta utilização do repositório Git, no qual deverá ser registrado todo o histórico da implementação por meio de *commits*, e;
- qualidade do relatório produzido

## Dúvidas e informações

Caso haja qualquer dúvida, questionamento ou necessidade de informação adicional, é possível:

- enviar *e-mail* para o endereço <everton.cavalcante@ufrn.br>;
- enviar mensagem privada diretamente ao docente, utilizando o servidor Discord;
- enviar mensagem no canal de texto `#duvidas` no servidor Discord, ou;
- agendar encontros síncronos pelo canal de áudio `Fale com Prof. Everton` no Discord.
