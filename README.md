# Wildfly - Domain ou Standalone

---

## Qual modelo usar?

É comum que ao escolhermos a utilização de uma plataforma como o Wildfly para a execução de nossos aplicativos Java, nos deparamos com a seguinte questão: "Qual modo de execução utilizar?", e a resposta é **depende**! O Wildfly possui 2 modos de execução, o domain e o standlone, e todo o seu cenário irá influenciar na escolha que deve ser feita, para ajudar na escolha algumas perguntas podem falicitar a decisão:

- Qual a quantidade de instâncias que será necessária?
- Será preciso um gerencimaneto centralizado e controle de configuração?
- Será preciso um ponto único e controlável de deployment das aplicações?
- As instâncias estarão espalhadas por diversas máquinas?

Com certeza respondendo essas perguntas você já terá um boa noção do que precisa, e para isso vamos entender melhor o que diferece cada modo de execução.

## Modo Standalone

O modo standalone, como o próprio nome sugere é uma instância única onde o Wildfly irá prover todos os recursos necessários para a execução do seu aplicativo java. Este módulo utiliza toda a estrutura de arquivos do Wildfly para si, assim não é possível executar outra instância utilizando a mesma estrutura, será necessário outro diretório standalone para realizar a execução de outra JVM.

Para o modo standalone ainda é possível contar com perfis de execução que são separados cada um em um arquivo xml diferente, estes podem ser escolhidos no momento da execução, onde pode-se escolher entre:

Perfil|Arquivo de configuração|Utilização
------|-----------------------|----------
Web|standalone.xml|Permite o uso do perfil Java EE Web
Full|standalone-full.xml|Permite o uso do perfil Java EE Full
Web c/ HA|standalone-ha.xml|Permite o uso do perfil Java EE Web com características de HA
Full c/ HA|standalone-full-ha.xml|Permite o uso do perfil Java EE Full com características de HA

> Os detalhes de cada perfil e exemplos de uso serão detalhados em um outro post.

Dessa forma vemos que neste modo o gerenciamento, deploy dos aplicativos e manutenção são individuais para cada instância tornando este trabalho custoso caso você tenha diversas instâncias para administrar.

## Modo Domain

Já neste modo é possível ter uma instância centralizadora que terá a função de  "domain controller", e as instâncias que irão receber as instruções que terão a função apenas de "host controller". Com o modo domain temos um ponto único de gerenciamento onde toda configuração realizada no "domain controller" é distribuída para as outras intâncias, evitando assim que uma nova instância seja criada com uma configuração indevida, terá também um ponto único de deploy dos aplicativos e pela configuração realizada o "domain controller" se encarregará de distribuir o artefato somente para as instâncias configuradas para recebê-lo.

Este modo, assim como o standalone também possui os mesmos perfis de execução, porém há uma diferença no nome e este é passado através da configuração e não de arquivos como no modo domain. As opções são:

Perfil|Nome do Profile|Utilização
Web|default|Permite o uso do perfil Java EE Web
Full|full|Permite o uso do perfil Java EE Full
Web c/ HA|ha|Permite o uso do perfil Java EE Web com características de HA
Full c/ HA|full-ha|Permite o uso do perfil Java EE Full com características de HA

Sabemos então que com o modo domain caso tenhamos diversas instâncias ou um ambiente onde é necessário um controle maior de gerenciamento, este modo irá facilitar muito mais o trabalho do administrador.

## Conclusão

Com base nessas informações, podemos responder as perguntas e chegar uma conclusão que o modo standalone pode ser a melhor escolha para um ambiente tanto de desenvolvimento rápido e ágil como de produção por ter uma configuração e execução mais simples fazendo com que o ambiente seja disponibilizado mais rapidamente, porém se seu cenário requerer diversas intâncias em diversos hosts isto pode se tornar um calcanhar de Aquiles, fazendo com que a gestão seja demasiada trabalhosa e dificultando as tarefas diárias.

Assim para maior robustez de um ambiente grande e/ou com políticas rigorosas de controle de gestão e acesso, o modo domain seria o mais indicado por provêr toda a gestão concentrada em um único ponto, gerando facilidade, agilidade e rapidez para o administrador destas intâncias gerenciar os serviços e realizar as tarefas diárias.

---

Esta é apenas uma leitura sintetizada sobre os modos de operação do Wildfly, nos próximos posts iremos aprofundar e ver mais detalhes sobre cada modo, seus perfis e casos de uso. Até a próxima.
