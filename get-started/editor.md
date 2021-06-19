# Configure um editor

Você pode construir aplicativos com Flutter usando qualquer editor de texto combinado com nossas ferramentas de linha de comando. 
No entanto, recomendamos o uso de um de nossos plug-ins de editor para uma experiência ainda melhor. Esses plug-ins fornecem autocompletar de códigos, 
destaque de sintaxe, assistências de edição de widget, suporte para execução e depuração e muito mais.

Siga as etapas abaixo para adicionar um plug-in de editor para Android Studio, IntelliJ, VS Code ou Emacs. Se você quiser usar um editor diferente, 
tudo bem, pule para a próxima etapa: Test drive.

## Android Studio e IntelliJ

#### Instale o Android Studio
O Android Studio oferece uma experiência IDE completa e integrada para Flutter.

* [Android Studio](https://developer.android.com/studio), versão 3.0 ou posterior

Como alternativa, você também pode usar o IntelliJ:

* [Comunidade IntelliJ IDEA](https://www.jetbrains.com/idea/download/), versão 2017.1 ou posterior
* [IntelliJ IDEA Ultimate](https://www.jetbrains.com/idea/download/), versão 2017.1 ou posterior

#### Instale os plug-ins Flutter e Dart
As instruções de instalação variam de acordo com a plataforma.

##### Mac
Use as seguintes instruções para macos:

1. Inicie o Android Studio.
2. Abra as preferências de plug- ins (**Preferences > Plugins** a partir de v3.6.3.0 ou posterior).
3. Selecione o plugin Flutter e clique em **Install**.
4. Clique em **Yes** quando solicitado a instalar o plug-in Dart.
5. Clique em **Restart** quando solicitado.

##### Linux ou Windows
Use as seguintes instruções para Linux ou WIndows:

1. Abra as preferências de plug-ins (**File > Settings > Plugins**).
2. Selecione **Marketplace**, selecione o plugin Flutter e clique em **Install**.

## Visual Studio Code
VS Code é um editor leve com suporte a execução de aplicativos Flutter e também suporte para depuração.

* [VS Code](https://code.visualstudio.com/), última versão estável

##### Instale os plug-ins Flutter e Dart

1. Inicie o código VS.
2. Abra **View > Command Palette…**.
3. Digite “install” e selecione **Extensions: Install Extensions**.
4. Digite “flutter” no campo de pesquisa de extensões, selecione **Flutter** na lista e clique em **Install** . Isso também instala o plug-in Dart necessário.

##### Valide sua configuração com o Flutter Doctor

1. Abra **View > Command Palette…**.
2. Digite “doctor” e selecione o **Flutter: Run Flutter Doctor**.
3. Revise a saída no painel **OUTPUT** para quaisquer problemas. Certifique-se de selecionar Flutter no menu suspenso nas diferentes opções de saída.

## Emacs
Emacs é um editor leve com suporte para Flutter e Dart.

* [Emacs](https://www.gnu.org/software/emacs/download.html), última versão estável

##### Instale o pacote lsp-dart
Para obter informações sobre como instalar e usar o pacote, consulte a documentação do [lsp-dart](https://emacs-lsp.github.io/lsp-dart/).
