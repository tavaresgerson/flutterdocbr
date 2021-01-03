# Instalação do Windows

## Requisitos do sistema

Para instalar e executar o Flutter, seu ambiente de desenvolvimento deve atender a estes requisitos mínimos:

+ Sistemas operacionais: Windows 7 SP1 ou posterior (64 bits), baseado em x86-64
+ Espaço em disco: 1.32 GB (não inclui espaço em disco para IDE/ferramentas).
+ Ferramentas: o Flutter depende dessas ferramentas estarem disponíveis em seu ambiente.
  + Windows PowerShell 5.0 ou mais recente (pré-instalado com o Windows 10)
  + Git para Windows 2.x, com a opção _Usar Git no prompt de comando do Windows_.

Se o Git para Windows já estiver instalado, certifique-se de executar os comandos do git no prompt de comando ou no PowerShell.

### Obtenha o Flutter SDK

* Baixe o seguinte pacote de instalação para obter a versão estável mais recente do Flutter SDK: [Download](https://storage.googleapis.com/flutter_infra/releases/stable/windows/flutter_windows_1.22.5-stable.zip)
* Para outros canais de lançamento e compilações mais antigas, consulte a página de [lançamentos do SDK](https://flutter.dev/docs/development/tools/sdk/releases).
* Extraia o arquivo zip e coloque o diretório `flutter` no local de instalação desejado para o Flutter SDK (por exemplo, `C:\src\flutter`).

> **Aviso:** Não instale o Flutter em um diretório como `C:\Program Files\aquele que requer privilégios elevados`.

Se você não quiser instalar uma versão fixa do pacote de instalação, pode pular as etapas 1 e 2. Em vez disso, obtenha o código-fonte do repositório Flutter no GitHub e altere branches ou tags conforme necessário. Por exemplo:

content_copy
C:\src>git clone https://github.com/flutter/flutter.git -b stable
Agora você está pronto para executar comandos Flutter no Console do Flutter.

### Atualize o caminho
Se você deseja executar ter comandos do Flutter no console normal do Windows, siga estas etapas para adicionar à variável de ambiente:

* No menu Iniciar pesquise 'env' e selecione **Editar variáveis de ambiente para sua conta**.
* Em **Variáveis do usuário**, verifique se há uma entrada chamada **Path**:
  * Se a entrada existir, anexe o caminho completo para usar `flutter\bin\;` com o separador dos valores existentes.
  * Se a entrada não existir, crie uma nova variável de usuário nomeada `Path` com o caminho completo para `flutter\bin` como seu valor.
* Você deve fechar e reabrir todas as janelas de console existentes para que essas alterações tenham efeito.

> Nota: A partir do lançamento dev 1.19.0 do Flutter, o Flutter SDK contém o comando dart junto com o 
> flutter para que você possa executar mais facilmente os programas de linha de comando do Dart. Baixar 
> o Flutter SDK também baixa a versão compatível do Dart, mas se você baixou o Dart SDK separadamente, 
> certifique-se de que a versão do `dart` no Flutter é a primeira em seu caminho, pois as duas versões 
> podem não ser compatíveis. O comando a seguir (no macOS, linux e Chrome OS) informa se os comandos `flutter` e `dart`
> se originam do mesmo diretório `bin` e, portanto, são compatíveis. (Algumas versões do Windows oferecem suporte a um comando `where`
> semelhante.)

```bash
 which flutter dart
  /path-to-flutter-sdk/bin/flutter
  /usr/local/bin/dart
```
> Conforme mostrado acima, os dois comandos não vêm do mesmo diretório `bin`. Atualize seu caminho para usar os 
> comandos anteriores `/path-to-flutter-sdk/bin` aos comandos `/usr/local/bin` (neste caso). Depois de atualizar 
seu shell para que a alteração tenha efeito, a execução do comando `which` ou `where` novamente deve mostrar que 
os comandos `flutter` e `dart` agora vêm do mesmo diretório.

```bash
which flutter dart
  /path-to-flutter-sdk/bin/flutter
  /path-to-flutter-sdk/bin/dart
```

Para aprender mais sobre o comando `dart`, execute `dart -h` partir da linha de comando ou consulte a página da ferramenta [dart](https://dart.dev/tools/dart-vm).

### Executar flutter doctor
Em uma janela de console que tem o diretório Flutter no caminho (veja acima), execute o seguinte comando para ver se há alguma dependência de plataforma necessária para concluir a configuração:

```bash
C:\src\flutter>flutter doctor
```

Este comando verifica seu ambiente e exibe um relatório do status da instalação do Flutter. Verifique a saída com cuidado 
para outro software que você possa precisar instalar ou outras tarefas a serem executadas (mostrado em **negrito**).

Por exemplo:

```bash
[-] Android toolchain - develop for Android devices
    • Android SDK at D:\Android\sdk
    ✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ
    • Try re-installing or updating your Android SDK,
      visit https://flutter.dev/setup/#android-setup for detailed instructions.
```

As seções a seguir descrevem como executar essas tarefas e concluir o processo de configuração. Depois de instalar todas as 
dependências ausentes, você pode executar o comando `flutter doctor` novamente para verificar se configurou tudo corretamente.

> Observação: se `flutter doctor` retornar que o plug-in Flutter ou o plug-in Dart do Android Studio não estão 
> instalados, vá para [Configurar um editor](https://flutter.dev/docs/get-started/editor?tab=androidstudio) para resolver esse problema.

> Aviso: a ferramenta `flutter` usa o Google Analytics para relatar anonimamente estatísticas de uso de recursos e 
> relatórios básicos de falha. Esses dados são usados para ajudar a melhorar as ferramentas do Flutter ao longo do tempo.
>
> A análise da ferramenta Flutter não é enviada na primeira execução. Para desativar o relatório, digite 
> `flutter config --no-analytics`. Para exibir a configuração atual, digite `flutter config`. Se você cancelar 
> o Analytics, um evento de cancelamento será enviado e nenhuma outra informação será enviada pela ferramenta Flutter.

Ao fazer o download do Flutter SDK, você concorda com os Termos de Serviço do Google. Observação: a Política de Privacidade 
do Google descreve como os dados são tratados neste serviço.

Além disso, o Flutter inclui o Dart SDK, que pode enviar métricas de uso e relatórios de falha para o Google.

### Configuração Android

> Nota: Flutter depende de uma instalação completa do Android Studio para fornecer 
> suas dependências de plataforma Android. No entanto, você pode escrever seus aplicativos
  Flutter em vários editores; uma etapa posterior discute isso.

#### Instale o Android Studio
* Baixe e instale o Android Studio .
* Inicie o Android Studio e siga o 'Android Studio Setup Wizard'. Isso instala o mais recente Android SDK, 
  Android SDK Command-line Tools e Android SDK Build-Tools, que são exigidos pelo Flutter ao desenvolver para Android.

#### Configure seu dispositivo Android

Par executar e testar seu aplicativo Flutter em um dispositivo Android, você precisa de um dispositivo 
Android com Android 4.1 (API de nível 16) ou superior.

* Ative as opções do desenvolvedor e a depuração USB em seu dispositivo. Instruções detalhadas estão disponíveis na documentação do Android.
* Apenas para Windows: Instale o driver USB do Google.
* Usando um cabo USB, conecte seu telefone ao computador. Se solicitado em seu dispositivo, autorize seu computador a acessar seu dispositivo.
* No terminal, execute o comando `flutter devices` para verificar se o Flutter reconhece seu dispositivo Android conectado. 
  Por padrão, o Flutter usa a versão do Android SDK onde sua adb ferramenta está baseada. Se quiser que o Flutter use uma 
  instalação diferente do Android SDK, você deve definir a variável `ANDROID_SDK_ROOT` nas variáveis de ambiente para esse diretório 
  de instalação.
  
#### Configure o emulador Android

Para executar e testar seu aplicativo Flutter no emulador Android, siga estas etapas:

* Ative a aceleração de VM em sua máquina.
* Inicie o **Android Studio**, clique no ícone **AVD Manager** e selecione **Create Virtual Device...**
  * Em versões anteriores do Android Studio, você deve iniciar **Android Studio > Tools > Android > AVD Manager** e selecionar
    **Create Virtual Device...**. (O submenu Android está presente apenas quando dentro de um projeto Android.)
  * Se você não tiver um projeto aberto, pode escolher **Configure > AVD Manager** e selecione **Create Virtual Device...**
* Escolha uma definição de dispositivo e selecione **Next**.
* Selecione uma ou mais imagens do sistema para as versões do Android que deseja emular e selecione **Next**. Uma imagem x86 ou x86_64 é recomendada.
* Em Desempenho emulado, selecione Hardware - GLES 2.0 para ativar a [aceleração de hardware](https://developer.android.com/studio/run/emulator-acceleration).
* Verifique se a configuração do AVD está correta e selecione Concluir.
  
  Para obter detalhes sobre as etapas acima, consulte [Gerenciando AVDs](https://developer.android.com/studio/run/managing-avds).

* No Android Virtual Device Manager, clique em Executar na barra de ferramentas. O emulador é inicializado e exibe a tela padrão 
  para a versão do sistema operacional e dispositivo selecionados.

#### Configuração da web
O Flutter tem suporte inicial para a construção de aplicativos da web usando o canal `beta` do Flutter. Para adicionar suporte 
para desenvolvimento web, siga estas [instruções](/get-started/install/web) quando você tiver concluído a configuração acima.

#### Próxima Etapa
Configure seu editor preferido.
