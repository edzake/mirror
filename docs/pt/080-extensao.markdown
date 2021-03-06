[chapter Extensão]

Agora que você conhece o Mirror, talvez você queira um pouco mais.

[section Reflection Providers]

Basicamente todo o trabalho sujo é feito por uma coleção de interfaces que chamamos de Reflection
Providers.

Esse é o núcleo real do Mirror.

Atualmente temos apenas ::net.vidageek.mirror.provider.java.PureJavaReflectionProvider::, que usa 
apenas a **Java Reflection API**. 

Mas você pode simplesmente implementar ::net.vidageek.mirror.provider.ReflectionProvider:: para ter mais
controle sobre o que está acontecendo.

Na verdade, ::net.vidageek.mirror.provider.ReflectionProvider:: é apenas um grande wrapper para interfaces
mais específicas:

[list]
* ::net.vidageek.mirror.provider.AnnotatedElementReflectionProvider.java::
* ::net.vidageek.mirror.provider.ClassReflectionProvider.java::
* ::net.vidageek.mirror.provider.ConstructorReflectionProvider.java::
* ::net.vidageek.mirror.provider.FieldReflectionProvider.java::
* ::net.vidageek.mirror.provider.MethodReflectionProvider.java::
[/list]

Mas como você faz para que o Mirror use seu Reflection Provider? De uma olhada em Extensão -> Configuração.

[section Sun Reflection Provider]

Existe uma implementação de ReflectionProvider que depende de algumas classes insternas da VM da Sun para 
acelerar as operações de reflection por ignorar as checagens de segurança. Este provider pode ser 25% mais
rápido que o provider padrão dependendo de como você usa o Mirror.

Aviso! Este provider provavelmente só funciona nas versões 1.5 e 1.6 das JVMs da Sun.

Existem duas formas de utilizar este provider:

[java]
new Mirror(new Sun15ReflectionProvider());
[/java]

Ou adicionar a seguinte linha ao seu mirror.properties:

[code]
provider.class = net.vidageek.mirror.provider.sun15.Sun15ReflectionProvider
[/code]


[section Configuração]

Existem duas formas de configurar o Mirror. Você pode instanciar Mirror passando um 
::net.vidageek.mirror.provider.ReflectionProvider:: :

[java]
new Mirror(new FakeReflectionProvider());
[/java]

Ou você pode deixar que o mirror leia um arquivo de configuração (mirror.properties) que deve ficar na 
pasta raiz do seu projeto.

Por enquanto, a única chave aceita neste arquivo de configuração é a seguinte:

[list]
* provider.class : Este é o nome completo da classe implementando ::net.vidageek.mirror.provider.ReflectionProvider::
que você quer que o Mirror use.
[/list]

Um exemplo:

[code]
provider.class = net.vidageek.mirror.fake.FakeProvider
[/code]

Apenas para lembrar, nenhuma configuração é necessária para usar o Mirror. Ele vai funcionar bem sem ela.
Apenas use-a quando "bem" não for suficiente para suas necessidades.
