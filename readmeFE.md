# Mobile App Cliente - Lincar

Este guia considera o uso do Lubuntu 19.04, mas este serve para qualquer versão atual do Ubuntu.
Nesse README há a configuração inicial para começar um projeto com Flutter.

As versões utilizadas foram:

<ul>
  <li>Flutter 1.9.1</li>
  <li>Dart 2.5.0</li>
  <li>Visual Studio Code 1.39.2</li>
  <li>Android Studio 3.9.5</li>
</ul>


## Instalação do Flutter

No Linux Ubuntu 19.04:

Em primeiro é necessário baixar a versão SDK do Flutter no link abaixo:
https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_v1.9.1+hotfix.6-stable.tar.xz

Em seguida extraia o arquivo na pasta pessoal, logo após execute o comando para alterar o valor da variável PATH permanentemente, pois será necessário para utilizar os comandos na sessão do terminal.

```bash
nano ~/.bashrc
export PATH="$PATH:$HOME/flutter/bin"
```
## Instalação do Android Studio

Baixe o instalador no link: 
https://developer.android.com/studio

Extraia o arquivo na pasta pessoal e execute o arquivo studio.sh que está dentro da pasta /bin.
Inicie o Android Studio e acesse o 'Assistente de instalação do Android Studio'. Isso instala o Android SDK exigido pelo Flutter ao desenvolver para o Android.

## Instalação do Visual Studio Code

Baixe o instalador no link: 
https://code.visualstudio.com/docs/?dv=linux64_deb

É RECOMENDADO instalar as extensões Dart no VSCode. Basta apertar CTRL+SHIFT+X e pesquisar por essas extensões e instalar.

## Etapa Final

Use o comando para verificar se existem dependências necessárias para a instalação:

```bash
flutter doctor
```
Caso ocorra pendência instale-as e execute o comando novamente para verificar se você configurou tudo corretamente.

Para executar o projeto basta usar o comando:
```bash
flutter run
```
Após será instalado as dependências do projeto e estará pronto para ser executado.
