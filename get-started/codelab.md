# Escreva seu primeiro aplicativo Flutter, parte 1

> Dica: este codelab o orienta na criação de seu primeiro aplicativo Flutter no celular. Você pode preferir tentar escrever
> seu primeiro aplicativo Flutter na web. Observe que se você [habilitou a web](/get-started/web.md), o aplicativo concluído funcionará apenas em 
> todos esses dispositivos!

Este é um guia para criar seu primeiro aplicativo Flutter. Se você estiver familiarizado com o código orientado a objetos e 
conceitos básicos de programação, como variáveis, loops e condicionais, poderá concluir este tutorial. Você não precisa de 
experiência anterior com Dart, programação móvel ou web.

Este codelab é a parte 1 de um codelab de duas partes. Você pode encontrar a [parte 2](https://codelabs.developers.google.com/codelabs/first-flutter-app-pt2) 
no Google Developers Codelabs (bem como uma cópia deste codelab, parte 1 ).

<p align="center">
  <img src="https://flutter.dev/assets/get-started/startup-namer-part-1-9db323d8383da0000c8be4e1a12e3d9ff6ab3a0eb8b86984451b329f1f3b4196.gif" width="300" />
</p>

## O que você construirá na parte 1

Você implementará um aplicativo simples que gera nomes a pedido de uma empresa que está iniciando. O usuário pode selecionar e 
desmarcar nomes, salvando os melhores. O código gera preguiçosamente 10 nomes por vez. Conforme o usuário desce, mais nomes são 
gerados. Não há limite de até onde um usuário pode descer.

O GIF animado mostra como o aplicativo funciona na conclusão da parte 1.

### O que você aprenderá na parte 1

* Como escrever um aplicativo Flutter que pareça natural no iOS, Android e na web
* Conhecer a estrutura básica de um aplicativo Flutter
* Encontrar e usar pacotes para estender as funcionalidades
* Usar hot-reload para um ciclo de desenvolvimento mais rápido
* Como implementar um widget com estado
* Como criar uma lista infinita carregada lentamente

Na parte 2 deste codelab, você adicionará interatividade, modificará o tema do aplicativo e adicionará a capacidade de navegar 
para uma nova tela (chamada de *route* no Flutter).

### O que você vai usar

Você precisa de dois softwares para concluir este laboratório: o Flutter SDK e um editor. Este codelab pressupõe o 
Android Studio, mas você pode usar seu editor preferido.

Você pode executar este codelab usando qualquer um dos seguintes dispositivos:

* Um dispositivo físico (Android ou iOS) conectado ao seu computador e definido para o modo de desenvolvedor
* O simulador iOS (requer a instalação de ferramentas Xcode)
* O emulador Android (requer configuração no Android Studio)
* Um navegador (o Chrome é necessário para depuração)

Se você deseja compilar seu aplicativo para rodar na web, você deve habilitar este recurso (que está atualmente em beta). 
Para habilitar o suporte na web, use as seguintes instruções:

```bash
flutter channel beta
flutter upgrade
flutter config --enable-web
```
Você só precisa executar o comando `config` uma vez. Depois de habilitar o suporte web, cada aplicativo Flutter que você criar 
também compila para a web. Em seu IDE no menu suspenso de dispositivos ou na linha de comando usando `flutter devices`, você deve 
ver agora o Chrome e o servidor Web listados. Essa configuração inicia automaticamente Chrome. O servidor Web inicia um servidor 
que hospeda o aplicativo para que você possa carregá-lo de qualquer navegador. Use o dispositivo Chrome durante o desenvolvimento 
para poder usar DevTools e o servidor da web quando quiser testar em outros navegadores. Para obter mais informações, consulte 
[Construindo um aplicativo da web com Flutter](https://flutter.dev/web) e [Escreva seu primeiro aplicativo Flutter na web](https://flutter.dev/docs/get-started/codelab-web).

## Etapa 1: crie o início do aplicativo Flutter

Crie um aplicativo Flutter simples e modelado, usando as instruções em [Introdução ao seu primeiro aplicativo Flutter](https://flutter.dev/docs/get-started/test-drive#create-app).
Nomeie o projeto **startup_namer** (em vez de *flutter_app*).

>  Dica: Se você não ver “New Flutter Project” como uma opção em seu IDE, certifique-se de ter os [plug-ins instalados para Flutter e Dart](https://flutter.dev/docs/get-started/editor).

Você irá editar o arquivo `lib/main.dart`, onde reside o código do Dart.

+ Substitua o conteúdo de `lib/main.dart`.
  Exclua todo o código de `lib/main.dart`. Substitua pelo código a seguir, que exibe “Hello World” no centro da tela.
  
```dart
// Copyright 2018 The Flutter team. All rights reserved.
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Welcome to Flutter'),
        ),
        body: Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

> Dica: Ao colar o código em seu aplicativo, o recuo pode ficar distorcido. Você pode corrigir isso com as seguintes ferramentas Flutter:
>
> * Android Studio e IntelliJ IDEA: Clique com o botão direito no código e selecione **Reformat Code with dartfmt**.
> * Código VS: Clique com o botão direito e selecione **Format Document&&.
> * Terminal: Executar `flutter format <filename>`.

Execute o aplicativo da maneira que sua IDE descreve. Você deverá ver a saída do Android, iOS ou web, dependendo do seu dispositivo.

<p align="center">
  <img src="https://flutter.dev/assets/get-started/android/hello-world-fadb9765c01d33f0fea92d7ac767e036ea90e9159335ea1841277bc6bef3a10a.png" />
</p>

> Dica: na primeira vez que você executar em um dispositivo físico, pode demorar um pouco para carregar. Depois disso, você pode usar 
> o hot-reload para atualizações rápidas. Salvar também executa uma recarga rápida se o aplicativo já estiver em execução. Ao executar 
> um aplicativo diretamente do console usando `flutter run`, digite `r` para executar o hot-reload.


### Observações
Este exemplo cria um aplicativo com material. Material é uma linguagem de design visual padrão em dispositivos móveis e na web. Flutter 
oferece um rico conjunto de widgets do material. É uma boa ideia ter uma entrada `uses-material-design: true` seção do flutter de seu 
arquivo `pubspec.yaml`. Isso permitirá que você use mais recursos do Material, como seu conjunto de ícones padrão.

* O método `main()` usa a notação arrow (=>). Use notação de seta para funções que sejam de uma linha.
* O aplicativo estende de `StatelessWidget`, o que o torna um widget. No Flutter, quase tudo é um widget, incluindo alinhamento, preenchimento e layout.
* O `Scaffoldwidget` da biblioteca do material, fornece uma barra de aplicativo padrão e uma propriedade body que contém a árvore do widget para a tela 
  inicial. A subárvore do widget pode ser bastante complexa.
* A principal tarefa de um widget é fornecer um método `build()` que descreve como exibir o widget e como os de outros widgets de nível inferior.
* O corpo para este exemplo consiste em um widget `Center` que contém um widget `Text`como filho. O widget `Center` alinha sua subárvore de 
  widget ao centro da tela.
  
## Etapa 2: use um pacote externo

Nesta etapa, você começará a usar um pacote de código aberto chamado `english_words`, que contém alguns milhares das palavras em 
inglês mais usadas, além de algumas funções de utilitário.

Você pode encontrar o pacote `english_words`, bem como muitos outros pacotes de código aberto, em [pub.dev](pub.dev).

1. 1O arquivo `pubspec.yaml` gerencia os assets e dependências de um aplicativo Flutter. Em `pubspec.yaml`, adicione `english_words` (3.1.5 ou superior) 
à lista de dependências:

```yaml
dependencies:            
   flutter:            
     sdk: flutter            
   cupertino_icons: ^0.1.2            
 + english_words: ^3.1.5
```

2. Ao visualizar o arquivo `pubspec.yaml` na visualização do editor do Android Studio, clique em **Pub get**. Isso 
puxa o pacote para o seu projeto. Você deve ver o seguinte no console:

```bash
flutter pub get
Running "flutter pub get" in startup_namer...
Process finished with exit code 0
```
O **Pub get** também gera automaticamente o arquivo `pubspec.lock` com uma lista de todos os pacotes puxados para o projeto e seus números de versão.

3. Em `lib/main.dart`, importe o novo pacote:

```dart
import 'package:flutter/material.dart';
import 'package:english_words/english_words.dart';
```

Conforme você digita, o Android Studio oferece sugestões de bibliotecas para importar. Em seguida, ele renderiza a string de 
importação em cinza, permitindo que você saiba que a biblioteca importada não está sendo usada (até o momento).

Use o pacote de palavras em inglês para gerar o texto em vez de usar a string “Hello World”:

```dart
class MyApp extends StatelessWidget {            
 @override            
 Widget build(BuildContext context) {            
+  final wordPair = WordPair.random();            
     return MaterialApp(            
       title: 'Welcome to Flutter',            
       home: Scaffold(            
@@ -16,7 +18,7 @@    
           title: Text('Welcome to Flutter'),            
       ),            
       body: Center(            
-       child: Text('Hello World'),            
+       child: Text(wordPair.asPascalCase),            
       ),            
      ),            
    );
```
> Nota: “Pascal case” (também conhecido como “upper camel case”), significa que cada palavra na string, 
> incluindo a primeira, começa com uma letra maiúscula. Portanto, “uppercamelcase” se torna “UpperCamelCase”.

5. Se o aplicativo estiver em execução, recarregue com hot-reload para atualizar o aplicativo em execução. 
Cada vez que você clica em hot-reload ou salva o projeto, você deve ver um par de palavras diferente, escolhido 
aleatoriamente, no aplicativo em execução. Isso ocorre porque o emparelhamento de palavras é gerado dentro do 
método de construção, que é executado sempre que `MaterialApp` requer renderização ou ao alternar a plataforma 
no Inspetor do flutter.

<p align="center">
  <img src="https://flutter.dev/assets/get-started/android/step2-45e5a16e59926599e09b25b1c6d37372f77b69151cbebd070d2f94f657b1abde.png" width="200"/>
  <img src="https://flutter.dev/assets/get-started/ios/step2-de9da90d2a90351c8d651c50f345c822472dbcd93cd8bad099e4edf2aa499c43.png" width="200" />
</p>

## Problemas?

Se o seu aplicativo não estiver funcionando corretamente, procure erros de digitação. Se você quiser experimentar algumas das 
ferramentas de depuração do Flutter, verifique o conjunto DevTools de ferramentas de depuração e criação de perfil. Se necessário, 
use o código nos links a seguir para voltar aos trilhos.

* [pubspec.yaml](https://raw.githubusercontent.com/flutter/codelabs/master/startup_namer/step2_use_package/pubspec.yaml)
* [lib/main.dart](https://raw.githubusercontent.com/flutter/codelabs/master/startup_namer/step2_use_package/lib/main.dart)

## Etapa 3: adicionar um widget com estado

Widgets sem estado são imutáveis, o que significa que suas propriedades não podem ser alteradas - todos os valores são finais.

Estado _ful_ são widgets que podem manter o estado e que pode mudar durante o tempo de vida. A implementação de um widget com estado 
requer pelo menos duas classes: 1) uma classe `StatefulWidget` que cria uma instância de 2) uma classe `State`. A classe `StatefulWidget` é, em si, 
imutável e pode ser descartada e regenerada, mas a classe `State` persiste durante a vida útil do widget.

Nesta etapa, você adicionará um widget com estado, `RandomWords` que cria sua classe `State` `_RandomWordsState`. Em seguida, você o usará `RandomWords`
como filho dentro do widget `MyApp` sem estado existente.

1. Crie o código padrão para um widget com estado.
  Em `lib/main.dart`, posicione o cursor após todo o código, digite **Enter** algumas vezes para começar em uma nova linha. Em sua IDE, 
  comece a digitar `stful`. O editor pergunta se você deseja criar um widget `Stateful`. Pressione `Enter` para aceitar. O código padrão 
  para duas classes aparece e o cursor é posicionado para você inserir o nome do seu widget com estado.

2. Digite `RandomWords` que será o nome do seu widget.
  O widget `RandomWords` faz pouco mais do que criar sua classe `State`.

  Depois de inserir `RandomWords`, o IDE atualiza automaticamente a classe `State` que a acompanha , nomeando-a para `_RandomWordsState`. Por padrão, 
  o nome da classe `State` é prefixado com uma barra inferior. Prefixar um identificador com um sublinhado reforça a privacidade na linguagem Dart 
  e é uma prática recomendada para objetos `State`.

  O IDE também atualiza automaticamente a classe de estado para estender `State<RandomWords>`, indicando que você está usando uma classe `State` genérica 
  especializada para uso com `RandomWords`. A maior parte da lógica do aplicativo reside aqui - ele mantém o estado do widget `RandomWords`. Esta classe 
  salva a lista de pares de palavras gerados, que aumenta infinitamente conforme o usuário rola e, na parte 2 deste laboratório, você verá pares de palavras 
  favoritos conforme o usuário os adiciona ou remove da lista, alternando o ícone de coração.

  Ambas as classes agora têm a seguinte aparência:

```dart
class RandomWords extends StatefulWidget {
  @override
  _RandomWordsState createState() => _RandomWordsState();
}

class _RandomWordsState extends State<RandomWords> {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

3. Atualize o método `build()` em `_RandomWordsState`:

```dart
// lib/main.dart (_RandomWordsState)

class _RandomWordsState extends State<RandomWords> {
    @override
    Widget build(BuildContext context) {
      final wordPair = WordPair.random();
      return Text(wordPair.asPascalCase);
    }
  }
```

Remova o código de geração de palavras `MyApp` fazendo as alterações mostradas na seguinte comparação:

```dart
// {step2_use_package → step3_stateful_widget} /lib/main.dart
@@ -10,7 +10,6 @@
	  class  MyApp  extends  StatelessWidget  {
	    @sobrepor
	    Construção de widget (contexto BuildContext) {
	-  última wordPair = WordPair.random ();    
	      return MaterialApp (
	        título: 'Bem-vindo ao Flutter' ,
	        casa: Scaffold (
@@ -18,8 +17,8 @@
	            title: const Text ( 'Bem-vindo ao Flutter' ),
	          ),
	          corpo: Centro (
-            criança:Texto(wordPair.asPascalCase),
+            filho:Palavras aleatórias(),
	          ),
	        ),
	      );
	    }
```

Reinicie o aplicativo. O aplicativo deve se comportar como antes, exibindo um par de palavras cada vez que você recarregar ou salvar o aplicativo.

> **Dica:** Se você ver um aviso em um hot reload informando que pode ser necessário reiniciar o aplicativo, considere reiniciá-lo. O aviso 
> pode ser um falso positivo, mas reiniciar seu aplicativo garante que suas alterações sejam refletidas na IU do aplicativo.

#### Problemas?
Se o seu aplicativo não estiver funcionando corretamente, procure erros de digitação. Se você quiser experimentar algumas das ferramentas de 
depuração do Flutter, verifique o conjunto [DevTools](https://flutter.dev/docs/development/tools/devtools) de ferramentas de depuração e criação de perfil. 
Se necessário, use o código no link a seguir para voltar aos trilhos.

* [lib/main.dart](https://raw.githubusercontent.com/flutter/codelabs/master/startup_namer_null_safety/step3_stateful_widget/lib/main.dart)

### Etapa 4: crie uma ListView de rolagem infinita
Nesta etapa, você expandirá `_RandomWordsState` para gerar e exibir uma lista de pares de palavras. Conforme o usuário rola, 
a lista (exibida em um `ListViewwidget`) cresce infinitamente. O construtor `ListView` de fábrica permite que você crie uma 
exibição de lista preguiçosamente, sob demanda.

1. Adicione uma lista `_suggestions` à classe `_RandomWordsState` para salvar pares de palavras sugeridas. Além disso, adicione uma variável `_biggerFont`
   para aumentar o tamanho da fonte.

```dart
// lib/main.dart
class _RandomWordsState extends State<RandomWords> {
  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18.0);
  // ···
}
```
  
  A seguir, você adicionará uma função `_buildSuggestions()` à classe `_RandomWordsState`. Este método cria o `ListView` que exibe o par de palavras sugerido.
  
  A classe `ListView` fornece uma propriedade de construtor `itemBuilder`, que é um construtor de fábrica e função de retorno de chamada especificada como 
  uma função anônima. Dois parâmetros são passados para a função - o `BuildContext`, e o iterador de linha `i`,. O iterador começa em 0 e aumenta cada vez 
  que a função é chamada. Ele é incrementado duas vezes para cada par de palavras sugerido: uma vez para `ListTile` e uma vez para `Divider`. Este modelo 
  permite que a lista sugerida continue crescendo conforme o usuário rola.

2. Adicione uma função `_buildSuggestions()` à classe `_RandomWordsState`:

```dart
// lib/main.dart (_buildSuggestions)

Widget _buildSuggestions() {
  return ListView.builder(
      padding: const EdgeInsets.all(16.0),
      itemBuilder: /*1*/ (context, i) {
        if (i.isOdd) return const Divider(); /*2*/

        final index = i ~/ 2; /*3*/
        if (index >= _suggestions.length) {
          _suggestions.addAll(generateWordPairs().take(10)); /*4*/
        }
        return _buildRow(_suggestions[index]);
      });
}
```
  O itemBuilderretorno de chamada é chamado uma vez por par de palavras sugeridas e coloca cada sugestão em uma ListTilelinha. Para linhas pares, a função adiciona uma ListTilelinha para o par de palavras. Para linhas ímpares, a função adiciona um Dividerwidget para separar visualmente as entradas. Observe que o divisor pode ser difícil de ver em dispositivos menores.
Adicione um widget divisor de um pixel de altura antes de cada linha no ListView.
A expressão é i ~/ 2dividida ipor 2 e retorna um resultado inteiro. Por exemplo: 1, 2, 3, 4, 5 torna-se 0, 1, 1, 2, 2. Isso calcula o número real de pares de palavras no ListView, menos os widgets divisores.
Se você atingiu o final dos pares de palavras disponíveis, gere mais 10 e adicione-as à lista de sugestões.
A _buildSuggestions()função chama _buildRow()uma vez por par de palavras. Esta função exibe cada novo par em a ListTile, o que permite tornar as linhas mais atraentes na próxima etapa.

Adicione uma _buildRow()função a _RandomWordsState:

lib / main.dart (_buildRow)
content_copy
Widget _buildRow ( WordPair pair ) { return ListTile ( 
    title : Text ( 
      pair . AsPascalCase , 
      style : _biggerFont , ), ); } 
    
    
  
Na _RandomWordsStateaula, atualize o build()método a ser usado _buildSuggestions(), em vez de chamar diretamente a biblioteca de geração de palavras. ( Scaffold implementa o layout visual básico do Material Design.) Substitua o corpo do método pelo código destacado:

lib / main.dart (build)
content_copy
@override
 Widget build ( BuildContext context ) { return Scaffold (   appBar : AppBar (     title : const Text ( 'Startup Name Generator' ), ),   body : _buildSuggestions (), ); } 
   
   
    
    
  
  
Na MyAppaula, atualize o build()método alterando o título e alterando a página inicial para ser um RandomWordswidget:

{step3_stateful_widget → step4_infinite_list} /lib/main.dart
@@ -10,15 +10,8 @@
1010	  class  MyApp  extends  StatelessWidget  {
1111	    @sobrepor
1212	    Construção de widget (contexto BuildContext) {
1313	      return MaterialApp (
14	-        título: 'Receber para Flutter' ,
15	-        casa:Andaime(
14	+        título: 'Comece Nome Gerador' ,
15	+        casa:Palavras aleatórias(),
16	-          appBar: AppBar (
17	-            title: const Text ( 'Bem-vindo ao Flutter' ),
18	-          ),
19	-          corpo: Centro (
20	-            criança: RandomWords (),
21	-          ),
22	-        ),
2316	      );
2417	    }
Reinicie o aplicativo. Você deve ver uma lista de pares de palavras, não importa o quão longe você role.

App na conclusão da quarta etapa no Android
Android
App na conclusão da quarta etapa no iOS
iOS
Problemas?
Se o seu aplicativo não estiver funcionando corretamente, procure erros de digitação. Se você quiser experimentar algumas das ferramentas de depuração do Flutter, verifique o conjunto DevTools de ferramentas de depuração e criação de perfil. Se necessário, use o código no link a seguir para voltar aos trilhos.

lib / main.dart
Perfil ou versão executada
 Importante: Do não testar o desempenho de seu aplicativo com debug e recarga quente habilitado.

Até agora, você está executando seu aplicativo no modo de depuração . O modo de depuração troca desempenho por recursos úteis para o desenvolvedor, como recarga a quente e depuração em etapas. Não é inesperado ver um desempenho lento e animações instáveis ​​no modo de depuração. Quando estiver pronto para analisar o desempenho ou lançar seu aplicativo, você vai querer usar os modos de construção “profile” ou “release” do Flutter. Para obter mais detalhes, consulte os modos de construção do Flutter .

 Importante: se você estiver preocupado com o tamanho do pacote do seu aplicativo, consulte Medindo o tamanho do seu aplicativo .

Próximos passos
O aplicativo da parte 2
O aplicativo da parte 2
Parabéns!

Você escreveu um aplicativo interativo Flutter que roda em iOS e Android. Neste codelab, você:

Criou um aplicativo Flutter do zero.
Código escrito do Dart.
Aproveitou uma biblioteca externa de terceiros.
Recarregamento a quente usado para um ciclo de desenvolvimento mais rápido.
Implementado um widget com estado.
Criou uma lista de rolagem infinita carregada lentamente.
Se desejar estender este aplicativo, prossiga para a parte 2 no site Google Developers Codelabs , onde você adiciona a seguinte funcionalidade:

Implemente a interatividade adicionando um ícone de coração clicável para salvar os pares favoritos.
Implemente a navegação para uma nova rota adicionando uma nova tela contendo os favoritos salvos.
Modifique a cor do tema, criando um aplicativo todo branco.
