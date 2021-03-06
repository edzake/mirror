[chapter Mirror]

O Mirror foi criado para resolver um simples problema, geralmente chamado de ReflectionUtil,
que está presente em quase todos os projetos que precisam de reflection para tarefas avançadas.

Trabalhar com a API de Reflection do Java é bem trabalhoso. Pergunte para qualquer pessoa que
você conhece que use reflection, e ele te dirá que é bem chato usá-lo.

Dê uma olhada no seguinte código:

[java]
// Vamos apenas definir o valor de um atributo. Deveria ser uma tarefa fácil, certo?

// "obj" é o objeto contendo o atributo que queremos definir o valor. 
Field toSet = null;
for (Field f : obj.getClass().getDeclaredFields()) { 
	// Busque todos os fields DECLARADOS na classe que define o objeto target 
	if (f.getName().equals("field")) {
		toSet = f;
	}
}
if (toSet != null && (toSet.getModifiers() & Modifier.STATIC) == 0) {
	toSet.setAccessible(true);
	toSet.set(target, value);
}
[/java]

Ah! Que código mais sujo! Completamente ilegível. O quê Modifier.STATIC está fazendo no meu código?

Então, o que um programador bom faria? Esconderia isso dentro de uma classe *Util, assim
ele poderia usar algo como:

[java]
ReflectionUtil.setField(target, fielName, value);
[/java]

Melhor, mas totalmente procedural. Ainda não está bom.

Não seria melhor se pudéssemos simplesmente dizer:

[code]
Caro programa,

Em um objeto target, defina o fieldName com value.
[/code]

Melhor, não?

Tirando todo o palavreado gentil e bonitinho, teríamos:

[java]
new Mirror().on(target).set().field(fieldName).withValue(value);
[/java]

E esse foi o nosso "Você nem sabia que isso era um tutorial" Tutorial. O Mirror é fácil assim.