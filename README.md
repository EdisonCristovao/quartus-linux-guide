#Quartus 

##Instalação Quartus e modelsim

Esse tutorial tem intuito de ajudar usuarios linux a instalar o programa quartus e modelsim.
Para usuarios windows, a instalação é feita normalmente e bem intuitiva.

###Obtenha o quartus

É possivel fazer o download direto no site da [Altera](http://dl.altera.com/?edition=lite).
O download pode ser feito em partes ou em um arquivo inteiro.
Esse tutorial foi criado e testado na versão 16.0, outras versoes podem geral erros de incompatibilidade com as lib's.

###Instalar dependencias

O software principal Quartus Prime é de 64 bits, um monte de ferramentas Altera enviados com Quartus Prime ainda são software de 32 bits. É por isso que nós precisamos instalar lotes de bibliotecas `lib32-` e outros programas. 

Se voce usa derivados de arch-linux, é necessario habilitar `multilib` editando o arquivo `/etc/pacman.conf`.

Os pacotes nativos necessarios sao  `expat fontconfig freetype2 xorg-fonts-type1 glibc gtk2 libcanberra libpng libpng12 libice libsm util-linux ncurses tcl tcllib zlib libx11 libxau libxdmcp libxext libxft libxrender libxt libxtst`.

Multiliib versão `lib32-expat lib32-fontconfig lib32-freetype2 lib32-glibc lib32-gtk2 lib32-libcanberra lib32-libpng lib32-libpng12 lib32-libice lib32-libsm lib32-util-linux lib32-ncurses lib32-zlib lib32-libx11 lib32-libxau lib32-libxdmcp lib32-libxext lib32-libxft lib32-libxrender lib32-libxt lib32-libxtst`

No arch-linux é possivel encontrar facilmente as lib's usando o comando `pacman` ou `yaourt`.

###Instalação

Depois de ter baixado o arquivo completo `Quartus-lite-16.0.0.211-linux.tar`, extraia o arquivo.
```tar -zxvf Quartus-lite-16.0.0.211-linux.tar```
Obtendo algo assim.
```
	*setup.sh
	*/componets
		*arria_lite-16.0.0.211.qdz
		*cyclonev-16.0.0.211.qdz  
		*max-16.0.0.211.qdz
		*QuartusHelpSetup-16.0.0.211-linux.run
		*cyclone-16.0.0.211.qdz
		*max10-16.0.0.211.qdz
		*ModelSimSetup-16.0.0.211-linux.run
		*QuartusLiteSetup-16.0.0.211-linux.run
```

O `setup.sh` precisa ter permisao de execução.

```
$ sudo chmod +x setup.sh
```
execute a instalação e siga os passos do assistente.

```
# ./setup.sh
```
Use o comando acima para iniciar a instalação.

a instalação padrao tentara instalar em `/root/altera/xx.x/`, recomenda-se que seja instalado em `/opt/altera/xx.x/`.

