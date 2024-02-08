### Capítulo 10
# Módulos

>"Escreva código fácil de deletar, não fácil de estender"
>
>—Tef, Programming is Terrible
<div style="text-align: right">
O programa ideal tem uma estrutura cristalina. É fácil de explicar, e cada parte desempenha um papel bem definido.

Um programa real típico cresce organicamente. Novas peças de funcionalidade são adicionadas conforme novas necessidades surgem. Estruturar - e preservar a estrutura - é trabalho adicional. É um trabalho que só compensará no futuro, na próxima vez que alguém trabalhar no programa. Portanto, é tentador negligenciá-lo e permitir que as partes do programa se tornem profundamente emaranhadas.

Isso causa dois problemas práticos. Primeiro, entender um sistema assim é difícil. Se todas as peças podem se tocar, é difícil olhar para qualquer uma isoladamente. Você é forçado a construir uma compreensão holística de todo o conjunto. Em segundo lugar, se você quiser usar qualquer funcionalidade desse programa em outra situação, reescrevê-lo pode ser mais fácil do que tentar desemaranhá-lo do seu contexto.

A expressão "grande bola de lama" é frequentemente usada para tais programas grandes e sem estrutura. Tudo fica grudado junto, e quando você tenta pegar uma peça, tudo se desfaz e suas mãos ficam sujas.
</div>
## Módulos

Os módulos são uma tentativa de evitar esses problemas. Um módulo é uma parte do programa que especifica quais outras partes ele depende e qual funcionalidade ele fornece para que outros módulos usem (sua interface).

As interfaces dos módulos têm muito em comum com as interfaces de objetos, como vimos no Capítulo 6. Elas disponibilizam parte do módulo para o mundo exterior e mantêm o restante privado. Ao restringir as maneiras pelas quais os módulos interagem entre si, o sistema se torna mais parecido com LEGO, onde as peças interagem através de conectores bem definidos, e menos como lama, onde tudo se mistura com tudo.

As relações entre os módulos são chamadas de dependências. Quando um módulo precisa de uma peça de outro módulo, diz-se que ele depende desse. Quando esse fato é claramente especificado no próprio módulo, ele pode ser usado para descobrir quais outros precisam estar presentes para poder usar um determinado módulo e para carregar automaticamente as dependências.

Para separar os módulos dessa maneira, cada um precisa ter seu próprio escopo privado.

Apenas colocar seu código JavaScript em arquivos diferentes não satisfaz esses requisitos. Os arquivos ainda compartilham o mesmo namespace global. Eles podem, intencional ou acidentalmente, interferir nos vínculos uns dos outros. E a estrutura de dependência permanece pouco clara. Podemos fazer melhor, como veremos mais adiante no capítulo.

Projetar uma estrutura de módulo adequada para um programa pode ser difícil. Na fase em que você ainda está explorando o problema, tentando diferentes abordagens para ver o que funciona, você pode não querer se preocupar muito com isso, já que pode ser uma grande distração. Uma vez que você tenha algo que pareça sólido, esse é um bom momento para dar um passo atrás e organizá-lo.