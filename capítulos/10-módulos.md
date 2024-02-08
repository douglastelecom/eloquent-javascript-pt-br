<div align='justify'>

### CAPÍTULO 10

# MÓDULOS

>"Escreva código fácil de deletar, não fácil de estender"
>
>—Tef, Programming is Terrible

![Módulos](../img/chapter_picture_10.jpg)

O programa ideal tem uma estrutura cristalina. É fácil de explicar, e cada parte desempenha um papel bem definido.

Um programa real típico cresce organicamente. Novas peças de funcionalidade são adicionadas conforme novas necessidades surgem. Estruturar - e preservar a estrutura - é trabalho adicional. É um trabalho que só compensará no futuro, na próxima vez que alguém trabalhar no programa. Portanto, é tentador negligenciá-lo e permitir que as partes do programa se tornem profundamente emaranhadas.

Isso causa dois problemas práticos. Primeiro, entender um sistema assim é difícil. Se todas as peças podem se tocar, é difícil olhar para qualquer uma isoladamente. Você é forçado a construir uma compreensão holística de todo o conjunto. Em segundo lugar, se você quiser usar qualquer funcionalidade desse programa em outra situação, reescrevê-lo pode ser mais fácil do que tentar desemaranhá-lo do seu contexto.

A expressão "grande bola de lama" é frequentemente usada para tais programas grandes e sem estrutura. Tudo fica grudado junto, e quando você tenta pegar uma peça, tudo se desfaz e suas mãos ficam sujas.



## MÓDULOS

Os módulos são uma tentativa de evitar esses problemas. Um módulo é uma parte do programa que especifica quais outras partes ele depende e qual funcionalidade ele fornece para que outros módulos usem (sua interface).

As interfaces dos módulos têm muito em comum com as interfaces de objetos, como vimos no Capítulo 6. Elas disponibilizam parte do módulo para o mundo exterior e mantêm o restante privado. Ao restringir as maneiras pelas quais os módulos interagem entre si, o sistema se torna mais parecido com LEGO, onde as peças interagem através de conectores bem definidos, e menos como lama, onde tudo se mistura com tudo.

As relações entre os módulos são chamadas de dependências. Quando um módulo precisa de uma peça de outro módulo, diz-se que ele depende desse. Quando esse fato é claramente especificado no próprio módulo, ele pode ser usado para descobrir quais outros precisam estar presentes para poder usar um determinado módulo e para carregar automaticamente as dependências.

Para separar os módulos dessa maneira, cada um precisa ter seu próprio escopo privado.

Apenas colocar seu código JavaScript em arquivos diferentes não satisfaz esses requisitos. Os arquivos ainda compartilham o mesmo namespace global. Eles podem, intencional ou acidentalmente, interferir nos vínculos uns dos outros. E a estrutura de dependência permanece pouco clara. Podemos fazer melhor, como veremos mais adiante no capítulo.

Projetar uma estrutura de módulo adequada para um programa pode ser difícil. Na fase em que você ainda está explorando o problema, tentando diferentes abordagens para ver o que funciona, você pode não querer se preocupar muito com isso, já que pode ser uma grande distração. Uma vez que você tenha algo que pareça sólido, esse é um bom momento para dar um passo atrás e organizá-lo.

## PACOTES

Uma das vantagens de construir um programa a partir de peças separadas e realmente poder executar essas peças individualmente é que você pode ser capaz de aplicar a mesma peça em diferentes programas.

Mas como você configura isso? Digamos que eu queira usar a função parseINI do Capítulo 9 em outro programa. Se for claro no que a função depende (neste caso, nada), posso simplesmente copiar todo o código necessário para o meu novo projeto e usá-lo. Mas então, se eu encontrar um erro nesse código, provavelmente vou corrigi-lo no programa com o qual estou trabalhando no momento e esquecer de corrigi-lo também no outro programa.

Uma vez que você comece a duplicar código, rapidamente perceberá que está desperdiçando tempo e energia movendo cópias ao redor e mantendo-as atualizadas.

Aí é onde entram os pacotes. Um pacote é um pedaço de código que pode ser distribuído (copiado e instalado). Ele pode conter um ou mais módulos e tem informações sobre quais outros pacotes depende. Um pacote geralmente também vem com documentação explicando o que ele faz, para que pessoas que não o escreveram ainda possam usá-lo.

Quando um problema é encontrado em um pacote ou uma nova funcionalidade é adicionada, o pacote é atualizado. Agora, os programas que dependem dele (que também podem ser pacotes) podem atualizar para a nova versão.

Trabalhar dessa maneira requer infraestrutura. Precisamos de um lugar para armazenar e encontrar pacotes e uma maneira conveniente de instalá-los e atualizá-los. No mundo JavaScript, essa infraestrutura é fornecida pelo NPM (https://npmjs.org).

O NPM é duas coisas: um serviço online onde é possível baixar (e enviar) pacotes e um programa (empacotado com o Node.js) que ajuda você a instalá-los e gerenciá-los.

No momento da escrita, existem mais de meio milhão de pacotes diferentes disponíveis no NPM. Uma grande parte deles é lixo, devo mencionar, mas quase todo pacote útil e publicamente disponível pode ser encontrado lá. Por exemplo, um analisador de arquivos INI, semelhante ao que construímos no Capítulo 9, está disponível sob o nome do pacote ini.

O Capítulo 20 mostrará como instalar esses pacotes localmente usando o programa de linha de comando npm.

Ter pacotes de qualidade disponíveis para download é extremamente valioso. Significa que muitas vezes podemos evitar reinventar um programa que 100 pessoas já escreveram antes e obter uma implementação sólida e bem testada pressionando algumas teclas.

Software é fácil e barato de copiar, então, uma vez que alguém o escreveu, distribuí-lo para outras pessoas é um processo eficiente. Mas escrevê-lo em primeiro lugar demanda trabalho, e responder às pessoas que encontraram problemas no código, ou que desejam propor novos recursos, é ainda mais trabalhoso.

Por padrão, você possui os direitos autorais sobre o código que escreve, e outras pessoas só podem usá-lo com sua permissão. Mas porque algumas pessoas são apenas gentis e porque publicar um bom software pode ajudar a torná-lo um pouco famoso entre os programadores, muitos pacotes são publicados sob uma licença que permite explicitamente que outras pessoas o usem.

A maioria do código no NPM é licenciada dessa forma. Algumas licenças exigem que você também publique o código que construiu em cima do pacote sob a mesma licença. Outras são menos exigentes, apenas exigindo que você mantenha a licença com o código conforme o distribui. A comunidade JavaScript geralmente usa o último tipo de licença. Ao usar pacotes de outras pessoas, certifique-se de estar ciente de sua licença.

## MÓDULOS IMPROVISADOS

Até 2015, a linguagem JavaScript não tinha um sistema de módulos integrado. No entanto, as pessoas estavam construindo sistemas grandes em JavaScript há mais de uma década e precisavam de módulos.

Então, eles projetaram seus próprios sistemas de módulos em cima da linguagem. Você pode usar funções JavaScript para criar escopos locais e objetos para representar interfaces de módulos.

Este é um módulo para ir entre nomes de dias e números (como retornados pelo método `getDay` do objeto `Date`). Sua interface consiste em `weekDay.name` e `weekDay.number`, e ele esconde os nomes de vínculo local dentro do escopo de uma expressão de função que é imediatamente invocada.

```js
const weekDay = function() {
  const names = ["Sunday", "Monday", "Tuesday", "Wednesday",
                 "Thursday", "Friday", "Saturday"];
  return {
    name(number) { return names[number]; },
    number(name) { return names.indexOf(name); }
  };
}();

console.log(weekDay.name(weekDay.number("Sunday")));
// → Sunday
```


</div>