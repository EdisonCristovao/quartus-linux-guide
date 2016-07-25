#Quartus   
  
  
##Instalação Quartus e Modelsim  
  
Esse tutorial tem intuito de ajudar usuários Linux a instalar o programa quartus e modelsim.  
Foi usada a distro manjaro baseada em arch para criar esse tutorial, outras distros são similares, mudando apenas configurações do sistema que podem se localizar em locais diferentes. 
Para usuários Windows, a instalação é feita normalmente e é bem intuitiva.  
  
###Obtenha o Quartus  
  
É possível fazer o download direto no site da [Altera](http://dl.altera.com/?edition=lite).  
O download pode ser feito em partes ou em um arquivo inteiro.  
Esse tutorial foi criado e testado na versão 16.0, mas funciona para qualquer versão. 
  
###Instalar dependências  
  
O software principal Quartus Prime é de 64 bits, varias ferramentas Altera enviados com Quartus Prime ainda são software de 32 bits. É por isso que nós precisamos instalar lotes de bibliotecas `lib32-` e outros programas.   
  
Se você usa derivados de arch-linux, é necessário habilitar `multilib` editando o arquivo `/etc/pacman.conf`.  
  
Os pacotes nativos necessários são  `expat fontconfig freetype2 xorg-fonts-type1 glibc gtk2 libcanberra libpng libpng12 libice libsm util-linux ncurses tcl tcllib zlib libx11 libxau libxdmcp libxext libxft libxrender libxt libxtst`.  
  
Multiliib versão `lib32-expat lib32-fontconfig lib32-freetype2 lib32-glibc lib32-gtk2 lib32-libcanberra lib32-libpng lib32-libpng12 lib32-libice lib32-libsm lib32-util-linux lib32-ncurses lib32-zlib lib32-libx11 lib32-libxau lib32-libxdmcp lib32-libxext lib32-libxft lib32-libxrender lib32-libxt lib32-libxtst`  
  
No arch-linux é possível encontrar facilmente as lib's usando o comando `pacman` ou `yaourt`.  
 
###Instalação 
 
Depois de ter baixado o arquivo completo `Quartus-lite-16.0.0.211-linux.tar`, extraia o arquivo. 
```$ tar -zxvf Quartus-lite-16.0.0.211-linux.tar``` 
Obtendo algo assim. 
``` 
setup.sh 
/componets 
arria_lite-16.0.0.211.qdz 
cyclonev-16.0.0.211.qdz   
max-16.0.0.211.qdz 
QuartusHelpSetup-16.0.0.211-linux.run 
cyclone-16.0.0.211.qdz 
max10-16.0.0.211.qdz 
ModelSimSetup-16.0.0.211-linux.run 
QuartusLiteSetup-16.0.0.211-linux.run 
``` 
 
O `setup.sh` precisa ter permissão de execução. 
 
``` 
$ sudo chmod +x setup.sh 
``` 
execute a instalação e siga os passos do assistente. 
 
``` 
# ./setup.sh 
``` 
Use o comando acima para iniciar a instalação. 
 
a instalação padrão tentara instalar em `/root/altera/xx.x/`, recomenda-se que seja instalado em `/opt/altera/xx.x/`. 
  
###Executando Quartus 
 
Assumindo que o quartus foi instalado em `/opt/altera/xx.x`, seu binário estará localizado em `/opt/altera/15.1/quartus/bin`. Rode quartus (64bits versão). 
``` 
$ /opt/altera/xx.x/quartus/bin/quartus --64bit 
``` 
ou 32 bits versão: 
``` 
$ /opt/altera/15.1/quartus/bin/quartus 
``` 

###Integrando Quartus com o Linux 
 
Tentando abrir o quartus com o comando `$ quartus` nota-se que o comando não existe, pode se criar o comando, criando um arquivo `quartus.sh` dentro da pasta `/etc/profile.d/`. 
 
``` 
/etc/profile.d/quartus.sh 
............................................... 
export PATH=$PATH:/opt/altera/xx.x/quartus/bin 
``` 
O arquivo precisa ser executável 
``` 
# chmod +x /etc/profile.d/quartus.sh 
``` 
Os scripts inseridos em `/etc/profile.d` na mesma sessão não funcionam sem reiniciar o sistema, para não precisar reiniciar pode-se executar o comando. 
``` 
$ source /etc/profile.d/quartus.sh 
``` 

###Atalho Application  
 
Também pode se criar um atalho na pasta application. Crie um arquivo `quartus.desktop` dentro da pasta `~/.local/share/applications`. 
``` 
~/.local/share/applications/quartus.desktop 
............................................... 
[Desktop Entry] 
Version=1.0 
Name=Quartus Prime Standard Edition vXX.X 
Comment=Quartus Prime design software for Altera FPGA's 
Exec=/opt/altera/xx.x/quartus/bin/quartus --64bit 
Icon=/opt/altera/xx.x/quartus/adm/quartusii.png 
Terminal=false 
Type=Application 
Categories=Development 
``` 
Não esquecer de alterar os "X" pela versão que estiver instalando. 
 
##Modelsim-Altera Edition 
 
###Instalação 
 
A instalação é feita junto com o quartus se você baixou a versão completa. Caso tenha baixado em partes, é preciso dar permissão de execução e iniciar a instalação. 
``` 
# ./modelsim.xx.x.run 
``` 
Se o diretório de instalação foi o `/opt`, então o modelsim foi instalado em `/opt/altera/15.1/modelsim_ase`. 
 
crie um comando para abrir o modelsim como foi feito com o quartus. 
 
``` 
vsim.sh 
.......................................... 
export PATH=$PATH:/opt/altera/xx.x/modelsim_ase/bin 
``` 
Para não reiniciar o sistema use `source`. 
``` 
$ source /etc/profile.d/vsim.sh 
``` 

###Compatibilidade 
  
Em algumas distros, ao iniciar modelsim com o comando `$ vsim`, gera o erro descrito abaixo. 
``` 
$ vsim 
Error: cannot find "/opt/altera/xx.x/modelsim_ase/bin/../linux_rh60/vsim" 
``` 
A solução é bem simples, edite o arquivo `vco` na linha 206, diretório `/opt/altera/xx.x/modelsim_ase/` como é sugerido. 
``` 
/opt/altera/xx.x/modelsim_ae/vco line 206 
 *)                vco="linux_rh60" ;; 
``` 
para 
``` 
/opt/altera/xx.x/modelsim_ae/vco line 206 
 *)                vco="linux" ;; 
``` 
Pode ser necessário permissão de escrita. 
 
### freetype2 2.5.0.1-1 
 
Ao atualizar o `freetype2` pode gerar erro na inicialização do modelsim. 
``` 
$ vsim 
Error in startup script: 
Initialization problem, exiting. 
Initialization problem, exiting. 
Initialization problem, exiting. 
   while executing 
"EnvHistory::Reset" 
   (procedure "PropertiesInit" line 3) 
   invoked from within 
"PropertiesInit" 
   invoked from within 
"ncFyP12 -+" 
   (file "/opt/questasim/linux_x86_64/../tcl/vsim/vsim" line 1) 
** Fatal: Read failure in vlm process (0,0) 
``` 
Existe três soluções possíveis. Você pode tentar um downgrade do pacote freetype2, você pode procurar a versão especifica na internet e instalar, ou você pode usar os libs que estão nesse repositório do git. 
Nesse tutorial será usada as libs disponíveis aqui nesse repositório. 
 
crie um arquivo `lib32` dentro de `/opt/altera/xx.x/modelsim_ase/` e execute os comandos. 
 
para entrar dentro da pasta criada.  
``` 
$ cd /opt/altera/xx.x/modelsim_ase/lib32 
``` 
Será necessário três arquivos que estão em `/lib`. 
``` 
libfreetype.so 
libfreetype.so.6 
libfreetype.so.6.10.2 ou libfreetype.so.6.10.1  
``` 
se os arquivos forem exatamente esses, copie para a pasta criada em `/opt/altera/xx.x/modelsim_ase/lib32` 
caso algum arquivo esteja mais atualizado, use os arquivos desse repositório executando o comando abaixo. 
``` 
$ wget https://github.com/JuniJoker/quartus-linux-guide/blob/master/libfreetype/libfreetype.tar.gz 
``` 
Extraia os arquivos 
``` 
$ tar -zxvf libfreetype.tar.gz 
``` 
Com as lib na pasta correta, edite o arquivo `vco` no diretório `/opt/altera/xx.x/modelsim_ase/` adicionando a linha abaixo depois de `#!/bin/bash` 
``` 
export LD_LIBRARY_PATH=/opt/altera/xx.x/modelsim_ase/lib32 
``` 
O script pode precisar de permisao de escrita. 
 
###Atalho Application 
 
Também pode se criar um atalho na pasta application. Crie um arquivo `modelsim.desktop` dentro da pasta `~/.local/share/applications`. 
``` 
~/.local/share/applications/modelsim.desktop 
............................................... 
[Desktop Entry] 
Version=1.0 
Name=ModelSim-Altera Edition 
Comment=ModelSim simulation software for Altera FPGA's 
Exec=/opt/altera/xx.x/modelsim_ae/bin/vsim 
Icon=/opt/altera/xx.x/modelsim_ae/modesim.gif 
Terminal=true 
Type=Application 
Categories=Development 
``` 
......................................................................................... 
 
 
Fonte [https://wiki.archlinux.org/index.php/Altera_Design_Software](https://wiki.archlinux.org/index.php/Altera_Design_Software). 
 
 
 
 
 
 