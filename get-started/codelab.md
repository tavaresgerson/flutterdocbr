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



