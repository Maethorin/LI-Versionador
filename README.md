# Versionador para os pacotes de Loja Integrada

O objetivo desse projeto é criar uma maneira fácil de subir e conhecer as versões dos pacotes da Loja Integrada que estão no https://pypi.python.org/pypi.
O que ele faz é incrementar a versão no arquivo setup.py do pacote e executar o comando 

    python setup.py sdist upload

na pasta do pacote. Ele não mexe no .pypirc e você tem que fazer as configurações necessárias para poder se conectar no PYPI. 

## Instalação

Ainda não fiz um script de instalação descente, mas vc pode baixar o projeto do GIT, entrar na raiz dele e instalar usando o develop:

    python setup.py develop

Depois disso, o comando **versionador** vai estar disponível no seu terminal

O próximo passo é criar o arquivo **versionador.conf**. Sua finalidade é explicada mais abaixo. 
Um modelo do arquivo fica na pasta src/config do projeto baixado do GIT. Basta copiar esse arquivo para o seguinte caminho:

    $HOME/.versionador/versionador.conf
    
Não se esqueça de criar a pasta .versionador no seu home.

O **versionador.conf** tem uma flag DEBUG que tem o valor padrão para True. Ela deverá ser trocada para True antes do **versionador** ser usado pra valer. Com essa flag False, ele faz tudo, mais não efetivamente envia o pacote para o PYPI.
  
## Opções

O comando **versionador** pode ser usando das seguintes maneiras:

### VERSIONANDO:

    versionador ab=-.-.+

para versionar o pacote de abreviatura **ab** ou:

    versionador pacote=-.-.+

para versionar o pacote de nome **pacote**

A regra do número de versões segue o seguinte padrão:

* Traço (-) o valor não será alterado
* Mais (+) o valor será incrementado em +1
* Número o valor será substituído pelo número especificado

Exemplos

    versionador ap=-.-.+ (se a versão atual for 0.3.4 a mova versão será 0.3.5)
    versionador ap=+.-.+ (se a versão atual for 0.3.0 a mova versão será 1.3.1)
    versionador ap=-.2.0 (se a versão atual for 0.1.4 a mova versão será 0.2.0)


### REGISTRANDO:

    versionador registrar pacote caminho-setup.py abreviatura

Para cadastrar novos pacotes a serem gerenciados pelo versionador.

O versionador usa o arquivo **versionador.conf** para manter os pacotes dos quais ele cuida. 
Quando a opçao **registrar** é passada, o versionador adiciona o pacote no arquivo **versionador.conf** onde.

* **pacote** - Nome escolhido por você para identificar o pacote no versionador apenas
* **caminho-setup.py** - O caminho completo para o arquivo setup.py do pacote que o versionador irá gerenciar.
* **abreviatura** - Uma sigla representando o pacote par facilitar na hora do versionamento.
    
### LISTANDO:

    versionador listar

Exemplo:

    PACOTE pagseguro      VERSÃO ATUAL  2.0.23 PARA VERSIONAR USE pagseguro=X.X.X      OU ps=X.X.X
    PACOTE paypal         VERSÃO ATUAL  2.0.10 PARA VERSIONAR USE paypal=X.X.X         OU pp=X.X.X
    PACOTE pagador        VERSÃO ATUAL  2.0.63 PARA VERSIONAR USE pagador=X.X.X        OU pg=X.X.X
    PACOTE koin           VERSÃO ATUAL  2.0.15 PARA VERSIONAR USE koin=X.X.X           OU ko=X.X.X
    PACOTE mptransparente VERSÃO ATUAL  0.0.20 PARA VERSIONAR USE mptransparente=X.X.X OU mt=X.X.X

para listar todos os pacotes ou:

    versionador requirements

para listar no formato do requirements.txt (nome-pacote==X.Y.Z) onde o nome do pacote é extraido do parâmetro **name** do **setup.py**.

Exemplo:

    li-pagador-pagseguro==2.0.23
    li-pagador-paypal==2.0.10
    li-pagador==2.0.63
    li-pagador-koin==2.0.15
    li-pagador-mercadopago-transparente==0.0.20

