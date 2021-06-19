# Mac OS

### requisitos de sistema
Para instalar e executar o Flutter, seu ambiente de desenvolvimento deve atender a estes requisitos mínimos:

* Sistemas operacionais: macOS (64 bits)
* Espaço em disco: 2,8 GB (não inclui espaço em disco para IDE / ferramentas).
* Ferramentas: Flutter usa `git` para instalação e atualização. Recomendamos instalar o [Xcode](https://developer.apple.com/xcode/), que inclui o `git`, mas você também pode 
  [instalar separadamente](https://git-scm.com/download/mac).

> Importante: se você estiver instalando em um Mac com o processador [Apple M1](https://www.apple.com/mac/m1) mais recente , 
> [essas notas complementares](https://github.com/flutter/flutter/wiki/Developing-with-Flutter-on-Apple-Silicon) podem ser útil, 
> pois oferecemos suporte completo para a nova arquitetura Apple Silicon.

### Obtenha o Flutter SDK
1. Baixe o seguinte pacote de instalação para obter a versão estável mais recente do Flutter SDK:

[flutter_macos_2.2.2-stable.zip](https://storage.googleapis.com/flutter_infra_release/releases/stable/macos/flutter_macos_2.2.2-stable.zip)

Para outros canais de lançamento e compilações mais antigas, consulte a [página de lançamentos](https://flutter.dev/docs/development/tools/sdk/releases) do SDK .

2. Extraia o arquivo no local desejado, por exemplo:
```bash
 cd ~/development
 unzip ~/Downloads/flutter_macos_2.2.2-stable.zip
```

3. Adicione a ferramenta `flutter` no seu path:

```bash
 export PATH="$PATH:`pwd`/flutter/bin"
```

Este comando define sua variável `PATH` apenas para a janela do terminal atual. Para adicionar o Flutter permanentemente, 
consulte [Atualizar seu path](https://flutter.dev/docs/get-started/install/macos#update-your-path).

Agora você está pronto para executar os comandos do Flutter!

> **Observação**: para atualizar uma versão existente do Flutter, consulte [Atualizando o Flutter](https://flutter.dev/docs/development/tools/sdk/upgrading).

#### Execute flutter doctor
Execute o seguinte comando para ver se há alguma dependência que você precisa instalar para concluir a configuração 
(para saída detalhada, adicione o sinalizador `-v`):

```bash
 flutter doctor
```

Este comando verifica seu ambiente e exibe um relatório na janela do terminal. O Dart SDK é fornecido com o Flutter; não é necessário instalar o 
Dart separadamente. Verifique a saída com cuidado para outro software que você possa precisar instalar ou outras tarefas a executar 
(mostrado em negrito ).

Por exemplo:

```bash
[-] Android toolchain - develop for Android devices
    • Android SDK at /Users/obiwan/Library/Android/sdk
    ✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ
    • Try re-installing or updating your Android SDK,
      visit https://flutter.dev/setup/#android-setup for detailed instructions.
```

As seções a seguir descrevem como executar essas tarefas e concluir o processo de configuração.

Depois de instalar todas as dependências ausentes, execute o comando `flutter doctor` novamente para verificar se você configurou tudo corretamente.

#### Baixar direto do GitHub em vez de usar um arquivo

_Isso é sugerido apenas para casos de uso avançados._

Você também pode usar o git diretamente em vez de baixar o arquivo preparado. Por exemplo, para baixar da branch estável:

```bash
 git clone https://github.com/flutter/flutter.git -b stable
```

Atualize seu path e execute `flutter doctor`. Isso permitirá que você saiba se há outras dependências que você precisa instalar 
para usar o Flutter (por exemplo, o Android SDK).

Se você não usou o arquivo, o Flutter baixará os binários de desenvolvimento necessários conforme necessário (se você usou o arquivo, eles serão incluídos 
no download). Você pode desejar fazer o pré-download desses binários de desenvolvimento (por exemplo, você pode desejar fazer isso ao configurar ambientes 
de [construção herméticos](https://sre.google/sre-book/release-engineering/) ou se tiver apenas disponibilidade de rede intermitente). 
Para fazer isso, execute o seguinte comando:

```bash
 flutter precache
```

Para opções adicionais de download, consulte `flutter help precache`.

> **Aviso**: a ferramenta `flutter` usa o Google Analytics para relatar anonimamente estatísticas de uso de recursos e [relatórios básicos de falha](https://github.com/flutter/flutter/wiki/Flutter-CLI-crash-reporting). 
> Esses dados são usados para ajudar a melhorar as ferramentas Flutter ao longo do tempo.
> 
> A análise da ferramenta Flutter não é enviada na primeira execução. Para desativar o relatório, digite `flutter config --no-analytics`. 
> Para exibir a configuração atual, digite `flutter config`. Se você cancelar o Analytics, um evento de cancelamento será enviado e nenhuma 
> informação adicional será enviada pela ferramenta Flutter.
> 
> Ao fazer o download do Flutter SDK, você concorda com os Termos de Serviço do Google. Observação: a [Política de Privacidade](https://policies.google.com/privacy) 
> do Google descreve como os dados são tratados neste serviço.
> 
> Além disso, o Flutter inclui o Dart SDK, que pode enviar métricas de uso e relatórios de falha para o Google.

#### Atualize seu path
Você pode atualizar sua variável PATH para a sessão atual na linha de comando, conforme mostrado em _Obtenha o Flutter SDK_. Você provavelmente desejará 
atualizar esta variável permanentemente, para que possa executar comandos `flutter` em qualquer sessão de terminal.

As etapas para modificar esta variável permanentemente para todas as sessões de terminal são específicas da máquina. Normalmente, você adiciona 
uma linha a um arquivo que é executado sempre que você abre uma nova janela. Por exemplo:

1. Determine o caminho do seu clone do Flutter SDK. Você precisa disso na Etapa 3.
2. Abra (ou crie) o arquivo `rc` para seu shell. Digite `echo $SHELL` em seu Terminal e isso informará qual shell você está usando. Se você estiver 
   usando o Bash, edite `$HOME/.bash_profile` ou `$HOME/.bashrc`. Se você estiver usando o Z Shell, edite `$HOME/.zshrc`. Se você estiver usando um 
   shell diferente, o caminho do arquivo e o nome do arquivo serão diferentes em sua máquina.
3. Adicione a seguinte linha e mude [PATH_OF_FLUTTER_GIT_DIRECTORY] para ser o caminho do seu clone do repositório git do Flutter:

```bash
 export PATH="$PATH:[PATH_OF_FLUTTER_GIT_DIRECTORY]/bin"
```

4. Execute `source $HOME/.<rc file>` para atualizar a janela atual ou abra uma nova janela de terminal para criar o arquivo automaticamente.
5. Verifique se o diretório `flutter/bin` está agora em seu PATH, executando:

```bash
 echo $PATH
```

Verifique se o comando `flutter` está disponível executando:

```bash
 which flutter
```

> **Nota:** A partir da versão 1.19.0 dev do Flutter, o Flutter SDK contém o comando `dart` junto com o comando `flutter` para que você possa executar 
> programas de linha de comando Dart com mais facilidade. Baixar o Flutter SDK também baixa a versão compatível do Dart, mas se você baixou o Dart SDK 
> separadamente, certifique-se de que a versão do dart do Flutter é a primeira em seu caminho, pois as duas versões podem não ser compatíveis. O comando 
> a seguir informa se os comandos `flutter` e se `dart` originam do mesmo diretório `bin` e, portanto, são compatíveis.
>
> ```bash
> which flutter dart
>  /path-to-flutter-sdk/bin/flutter
>  /usr/local/bin/dart
> ```
> Conforme mostrado acima, os dois comandos não vêm do mesmo diretório `bin`. Atualize seu caminho para usar os comandos `/path-to-flutter-sdk/bin` 
> anteriores aos comandos `/usr/local/bin` (neste caso). Depois de atualizar seu shell para que a alteração tenha efeito, a execução do comando `which`
> novamente, e isso deve mostrar que os comandos `flutter` e `dart` agora vêm do mesmo diretório.
>
> ```bash
> which flutter dart
>  /path-to-flutter-sdk/bin/flutter
>  /path-to-flutter-sdk/bin/dart
> ```
>Para aprender mais sobre o comando `dart`, execute `dart -h` partir da linha de comando ou consulte a página de [ferramentas do dart](https://dart.dev/tools/dart-vm).

### Configuração da plataforma
O macOS oferece suporte ao desenvolvimento de aplicativos Flutter no iOS, Android e na web (versão de visualização técnica). Conclua pelo menos uma das 
etapas de configuração da plataforma agora, para poder construir e executar seu primeiro aplicativo Flutter.

### configuração iOS

#### Instale o Xcode
Para desenvolver aplicativos Flutter para iOS, você precisa de um Mac com o Xcode instalado.

1. Instale a versão estável e mais recente do Xcode (usando o download da web ou a Mac App Store).
2. Configure as ferramentas de linha de comando do Xcode para usar a versão recém-instalada do Xcode executando a seguinte na linha de comando:

```bash 
 sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
 sudo xcodebuild -runFirstLaunch
```

Este é o caminho correto para a maioria dos casos, quando você deseja usar a versão mais recente do Xcode. Se você precisar usar uma versão 
diferente, especifique esse caminho.

3. Certifique-se de que o contrato de licença do Xcode seja assinado abrindo o Xcode uma vez e confirmando ou executando a `sudo xcodebuild -license` 
   partir da linha de comando.

Versões anteriores à versão estável mais recente ainda podem funcionar, mas não são recomendadas para o desenvolvimento do Flutter. O uso de versões 
antigas do Xcode para bitcode de destino não é compatível e provavelmente não funcionará.

Com o Xcode, você poderá executar aplicativos Flutter em um dispositivo iOS ou no simulador.

#### Configure o simulador iOS
Para se preparar para executar e testar seu aplicativo Flutter no simulador iOS, siga estas etapas:

1. Em seu Mac, encontre o Simulator via Spotlight ou usando o seguinte comando:

```bash
 open -a Simulator
```

2. Certifique-se de que seu simulador esteja usando um dispositivo de 64 bits (iPhone 5s ou posterior) verificando as configurações no 
   menu **Hardware** > **Device**.
   
3. Dependendo do tamanho da tela da sua máquina de desenvolvimento, dispositivos iOS de alta densidade de tela simulados podem sobrecarregar sua tela. 
   Pegue no canto do simulador e arraste-o para alterar a escala. Você também pode usar as opções **Window** > **Physical Size** ou **Window** > **Pixel Accurate** 
   se a resolução do seu computador for alta o suficiente.
   
   a) Se você estiver usando uma versão do Xcode anterior a 9.1, deverá definir a escala do dispositivo no menu **Window** > **Scale**.

### Crie e execute um aplicativo Flutter simples
Para criar seu primeiro aplicativo Flutter e testar sua configuração, siga estas etapas:

1. Crie um novo aplicativo Flutter executando o seguinte na linha de comando:

```bash
 flutter create my_app
```

2. Um diretório `my_app` é criado, contendo o aplicativo inicial do Flutter. Entre neste diretório:

```bash
 cd my_app
```

3. Para iniciar o aplicativo no Simulator, verifique se o Simulator está em execução e digite:

```bash
 flutter run
```

#### Deploy em dispositivos iOS
Para implantar seu aplicativo Flutter em um dispositivo iOS físico, você precisará configurar a implantação de dispositivo físico no Xcode e ter uma conta 
de desenvolvedor da Apple. Se o seu aplicativo estiver usando plug-ins Flutter, você também precisará do gerenciador de dependência de terceiros CocoaPods.

1. Você pode pular esta etapa se seus aplicativos não dependerem de plug-ins Flutter com código iOS nativo. [Instale e configure CocoaPods](https://guides.cocoapods.org/using/getting-started.html#installation) executando os seguintes comandos:

```bash
 sudo gem install cocoapods
```

> **Nota**: A versão padrão do Ruby requer `sudo` para a instalação da gem CocoaPods. Se você estiver usando um gerenciador de versões Ruby, pode ser 
> necessário executar ele sem `sudo`.

2. Siga o fluxo de assinatura do Xcode para provisionar seu projeto:
  a. Abra o espaço de trabalho padrão do Xcode em seu projeto executando `open ios/Runner.xcworkspace` em uma janela de terminal a partir do diretório do projeto Flutter.
  b. Selecione o dispositivo que você pretende implantar no menu suspenso de dispositivos próximo ao botão Executar.
  c. Selecione o projeto `Runner` no painel de navegação esquerdo.
  d. Na página `Runner` de configurações de destino, certifique-se de que sua equipe de desenvolvimento esteja selecionada em **Signing & Capabilities** > **Team**.
  
  Quando você seleciona uma equipe, o Xcode cria e baixa um certificado de desenvolvimento, registra seu dispositivo com sua conta, cria e baixa um perfil de 
  provisionamento (se necessário).
  
  + Para iniciar seu primeiro projeto de desenvolvimento iOS, talvez você precise entrar no Xcode com seu ID Apple. 
    
    <p align="center">
      <img src="/assets/xcode-account.png" />
    </p>

  O desenvolvimento e o teste são suportados por qualquer ID Apple. É necessário se inscrever no Apple Developer Program para distribuir seu aplicativo na 
  App Store. Para obter detalhes sobre os tipos de associação, [consulte Escolhendo uma associação](https://developer.apple.com/support/compare-memberships).
  
  + Na primeira vez que você usa um dispositivo físico conectado para o desenvolvimento do iOS, precisa confiar em seu Mac e no Certificado de Desenvolvimento 
    desse dispositivo. Selecione `Trust` na caixa de diálogo ao conectar pela primeira vez o dispositivo iOS ao Mac.
    
    <p align="center">
      <img src="/assets/trust-computer.png" />
    </p>
    
    Em seguida, vá para Configurações no dispositivo iOS, selecione **General > Device Management** e confie em seu certificado. Para usuários iniciantes, 
    pode ser necessário selecionar **General > Profiles > Device Management**.
    
  + Se a assinatura automática falhar no Xcode, verifique se o valor **General > Identity > Bundle Identifier** do projeto é exclusivo. Verifique o ID 
    do pacote do aplicativo
    
    <p align="center">
      <img src="/assets/xcode-unique-bundle-id.png" />
    </p>

3. Inicie seu aplicativo executando o comando `flutter run` ou clicando no botão Executar no Xcode.

### Configuração Android

> **Nota:** O Flutter depende de uma instalação completa do Android Studio para fornecer suas dependências de plataforma Android. No entanto, 
> você pode escrever seus aplicativos Flutter em vários editores; em uma etapa posterior discutiremos isso.

#### Instale o Android Studio

1. Baixe e instale o [Android Studio](https://developer.android.com/studio).
2. Inicie o Android Studio e siga o 'Android Studio Setup Wizard'. Isso instala o Android SDK, as ferramentas de linha de comando do 
   Android SDK e as ferramentas de construção do Android SDK, que são exigidas pelo Flutter ao desenvolver para Android.

#### Configure seu dispositivo Android
Para se preparar para executar e testar seu aplicativo Flutter em um dispositivo Android, você precisa de um dispositivo Android com 
Android 4.1 (API de nível 16) ou superior.

1. Habilite as **Opções do desenvolvedor** e a **Depuração USB** em seu dispositivo. Instruções detalhadas estão disponíveis na [documentação do Android](https://developer.android.com/studio/debug/dev-options).
2. Apenas para Windows: Instale o [driver USB do Google](https://developer.android.com/studio/run/win-usb).
3. Usando um cabo USB, conecte seu telefone ao computador. Se solicitado em seu dispositivo, autorize seu computador a acessar seu dispositivo.
4. No terminal, execute o comando `flutter devices` para verificar se o Flutter reconhece seu dispositivo Android conectado. Por padrão, o 
   Flutter usa a versão do Android SDK onde sua ferramenta `adb` está baseada. Se você deseja que o Flutter use uma instalação diferente do Android SDK, 
   defina a variável de ambiente `ANDROID_SDK_ROOT` para esse diretório de instalação.

#### Configure o emulador Android
Para se preparar para executar e testar seu aplicativo Flutter no emulador Android, siga estas etapas:

1. Ative a aceleração de VM em sua máquina.
2. Inicie o **Android Studio**, clique no ícone **AVD Manager** e selecione **Create Virtual Device…**
  * Em versões anteriores do Android Studio, você deve iniciar **Android Studio > Tools > Android > AVD Manager** e selecionar **Create Virtual Device…**. 
  (O submenu Android está presente apenas quando está dentro de um projeto Android.)
  
  * Se você não tiver em um projeto aberto, pode escolher **Configure > AVD Manager** e selecionar **Create Virtual Device...**
3. Escolha uma definição de dispositivo e selecione **Next**.
4. Selecione uma ou mais imagens do sistema para as versões do Android que deseja emular e selecione **Next**. Uma imagem x86 ou x86_64 é recomendada.
5. Em Desempenho emulado, selecione **Hardware - GLES 2.0** para ativar a [aceleração de hardware](https://developer.android.com/studio/run/emulator-acceleration).
6. Verifique se a configuração do AVD está correta e selecione **Finish**.

  Para obter detalhes sobre as etapas acima, consulte [Gerenciando AVDs](https://developer.android.com/studio/run/managing-avds).

7. No Android Virtual Device Manager, clique em Executar na barra de ferramentas. O emulador é inicializado e exibe a tela padrão para a versão do 
   sistema operacional e dispositivo selecionados.

### configuração do macOS

> **Aviso: Beta!** Esta área cobre o suporte para desktop, que está disponível como uma versão beta. O suporte beta ainda tem lacunas de recursos notáveis, 
> incluindo suporte de acessibilidade. Você pode tentar um snapshot beta do suporte para desktop no canal Stable, ou você pode acompanhar as últimas mudanças 
> para desktop no canal beta. Para obter mais informações, consulte a seção **Desktop** em [O que há de novo no Flutter 2](https://medium.com/flutter/whats-new-in-flutter-2-0-fe8e95ecc65)
> , um artigo gratuito no Medium.

#### Requisitos adicionais do macOS
Para o desenvolvimento de desktop do macOS, você precisa do seguinte, além do Flutter SDK:

* [Xcode](https://developer.apple.com/xcode/)
* [CocoaPods](https://cocoapods.org/) se você pretende usar plug-ins

#### Habilitar suporte para desktop
Na linha de comando, execute o seguinte comando para habilitar o suporte a desktop

```bash
 flutter config --enable-macos-desktop
```

Para obter mais informações, consulte [Suporte de desktop para Flutter](https://flutter.dev/desktop).

#### Configuração da web
O Flutter tem suporte para a construção de aplicativos da web no canal `stable`. Qualquer aplicativo criado no Flutter 2 é construído automaticamente para 
a web. Para adicionar suporte da web a um aplicativo existente, siga as instruções em [Construindo um aplicativo da web com Flutter](https://flutter.dev/docs/get-started/web)
ao concluir a configuração acima.
