# Guia de instalação dos softwares mais essenciais de trabalho no Ubuntu 22.04

## Softwares a serem instalados:

Para produtividade:

1. VScode;
2. Python3;
3. Jupyter notebook;

Para visualização e manipulação de estruturas:
1. VESTA;
2. XcrysDen;
3. Atomic Simulation Environment (ASE);
4. VMD;

Implementações de DFT:
1. SIESTA;
2. Quantum ESPRESSO;

### 2. Instalação do XcrysDen:
Para informações completas sobre o software, consulte (http://www.xcrysden.org)[http://www.xcrysden.org].

1. Baixar o arquivo compactado com os códigos pré-compliados (binário) do xcrysden versão 1.6 para linux 64 bits: (http://www.xcrysden.org/Download.html)[http://www.xcrysden.org/Download.html] ou:
```
wget http://www.xcrysden.org/download/xcrysden-1.6.2-linux_x86_64-shared.tar.gz
```
Antes de prosseguir, é importante instalar e se certificar que todas as dependências estão presentes, para que o programa possa funcionar da maneira correta. O XcrysDen depende das seguintes bibliotecas:
- libtk8.6;
- libtcl8.6;
- libTogl;
- libGLU
- libGL;
- libfftw3;
- libXmu
- libgfortran5

Outras recomendações são:
- Imagemagick;
- Openbabel;

As dependências necessárias e recomendadas podem ser instaladas com:
```
sudo apt install tk libglu1-mesa libtogl2 libfftw3-3 libxmu6 imagemagick openbabel libgfortran5
```

Após a instalação de todas as dependências, descompactar o arquivo do xcrysden:
```
tar -xv xcrysden-1.x.x
```
substituindo `xcrysden-1.x.x` com o nome completo do arquivo compactado baixado. Após descompactação, basta entrar na pasta do xcrysden e executar o arquivo binário **xcrysden** com: `./xcrysden`. Se tudo der certo, a janela do software deve abrir normalmente.

**IMPORTANTE**: Pode ocorrer um erro ao tentar abrir o programa pela primeira vez com a seguinte mensagem:
```
Running on platform : unix
   Operating system : Linux
Package ImageMagick's convert: /usr/bin/convert
Package ImageMagick's import: /usr/bin/import
Executing: /tmp/xcrysden-1.6.2-bin-shared/bin/ftnunit
Error in startup script: 
Couldn't configure togl widget
    while executing
"togl .mesa  -width          400  -height         400  -ident          .mesa  -rgba           $toglOpt(rgba)           -redsize        $toglOpt(redsize..."
    (procedure "PlaceGlobWin" line 107)
    invoked from within
"PlaceGlobWin 0 [expr round(670 * $fac1)] [expr round(670 * $fac1)]"
    (procedure "ViewMol" line 25)
    invoked from within
"ViewMol ."
    invoked from within
"if { [llength $argv] > 2 } {
    parseComLinArg [lrange $argv 2 end]
} else {
    ViewMol .
}"
    (file "/tmp/xcrysden-1.6.2-bin-shared/Tcl/xcInit.tcl" line 633)
```
Esse erro esta relacionado à imcompatibilidade entre o funcionamento do software (Xorg) com o sistema operacional (que por padrão é o Wayland). Para corrigir este erro, basta abrir o arquivo `/etc/gdm3/custom.conf` e descomentar a linha: `#WaylandEnable=false`. Depois, reinicie o sistema (que pode ser feito pelo terminal com `sudo reboot`). 

**ATENÇÃO! MUITO CUIDADO PARA NÃO ALTERAR MAIS NENHUMA LINHA DOS ARQUIVOS MENCIONADOS, UMA VEZ QUE ISSO PODE OCASIONAR COMPORTAMENTO INESPERADO DO UBUNTU.**

Isso deve ser suficiente para que o software funcione corretamente.

### 3. Instalação do ASE
Para maiores informações e acesso ao manual do software, acesse: (https://wiki.fysik.dtu.dk/ase/)[https://wiki.fysik.dtu.dk/ase/].
Para o funcionamento do ASE, é necessario ter instalado:
- Python 3.6 (ou mais recente);
- Numpy;
- SciPy;
- Matplotlib;

As três últimas dependências podem ser instaladas com o `pip`:
```
pip install numpy
pip install scipy
pip install matplotlib
```
Depois de instalar as dependências, o ASE pode ser instalado com o comando:
```
pip install --upgrade --user ase
```
### Método alternativo para instalar o ASE utilizando o conda:

```
# Criar um novo environment (altamante recomendado para evitar conflitos):
conda create -n ase
conda activate ase
conda install -y -c conda-forge
```

## Instalação SIESTA:
A forma mais simples de instalar o SIESTA em paralello é utilizar o conda:
```
conda create -n siesta
conda activate siesta
conda install -y -c conda-forge "siesta=*=*openmpi*"
```
Todas as dependências serão instaladas e o siesta poderá ser rodado cem paralelo com o ccomando:
```
OMP_NUM_THREADS=1 siesta < input.fdf > job.out
````

## Instalação do Quantum ESPRESSO:

```
conda create -n qespresso
conda activate qespresso
conda install -y -c conda-forge qe
```



