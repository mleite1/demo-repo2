#Operando no Git/Github

##Configurando chave SSH

Para efetuar push diretamente ao seu diretório no Github, você precisa provar ao site que você é o dono do repositório, ou pelo menos um contribuidor.
A autenticação da sua máquina é feita com a utilização de chaves SSH.

###1 - Criar chave SSH: abra seu terminal e digite o seguinte comando.
    $ ssh-keygen -t rsa -b 4096 -C "e-mail da conta no Github"
###2 - A chave será criada no diretório do seu usuário (em sua máquina) "users/fulano/.ssh/id_rsa", por padrão ela será nomeada como id_rsa, porém neste momento o será perguntado se você quer dar um nome específico a esta chave que está sendo criada.
###3 - Após a definição do nome da chave será perguntado se deseja adicionar uma senha a mesma.
###4 - Listar a chave para confirmação de sua criação. Caso tenha dado um nome específico a chave substitua id_rsa pelo nome escolhido.
    $ ls | grep id_rsa
###5 - Serão listados dos arquivos id_rsa (ou nome ecolhido para chave), um sem nehuma extensão e outro com a extensão ".pub", essa segunda chave é a chave pública que deve ser associada à sua conta no github para que o site possa reconhecer sua máquina como sendo confiável. A chave sem a extensão .pub é sua chave privada e nunca deve ser compartilhada.
###6 - Imprima a chave no terminal para poder copiar e fazer a associação no github.
    $ cat id_rsa.pub

    Exemplo de saída:
    > ssh-rsa asujhdhaiuhiodajidajioijoadjiaijojisijd ..... email@exemple.com
###7 - No seu perfil no github.com, vá em Configurações > SSH and GPG keys > Nova chave SSH.
    É possível adicionar um título ou nome a chave, no segundo campo adicionar a chave que foi copiada do terminal.
###8 - Adicionar a sua chave SSH à um agente SSH.
    8.1 - Inicie o agente SSH
        $ eval "$(ssh-agent -s)"
        > Agent pid 59566
    8.2 - Adicione sua chave privada ao agente SSH
        $ ssh-add -K ~/.ssh/id_rsa
    8.3 - Verifique se sua chave foi adicionada ao agente SSH
        $ ssh-add -l

##Base para operar no Github

###Checar se o Git está instalado
    $ git --version

###Iniciar um traking do Git em um repositório que ainda não está no Github
    $ git init

###Associar a pasta local à um repositório que se encontra criado no Github
    $ git remote add origin (página do git pegando o endereço SSH)

###Mostrar repositório remoto conectado ao repositório local
    $ git remote -v

###Pull repositório do Github
    $ git clone (página do git pegando o endereço SSH)

###Comando para listar arquivos incluindo ocultos
    $ ls -la

###Mostrar o status de alteração dos arquivos que não foram salvos no commit (tanto alterações quanto criação de novos arquivos)
    $ git status

###Adicionar arquivos novos ou aterações no Git
    $ git add ("." ou "nome do arquivo", na primeira opção são adicionados todos os arquivos)

###Efetuar commit para criação de ID que permita o rastreamento de histórico de alteração (no geral são adicionadas duas mensagens para identificar a alteração efetuada usando "-m" e a mensagem entre áspas)
    $ git commit -m "Título" -m "Descritivo"

###Commit live no Github
    $ git push origin main


##Procedimento padrão de push:
    - Verificar status   > Adicionar alterações ao Git   > Verificar status   > Commit                                                                         > Commit live no Github
    - $ git status       > $ git add .                   > $ git status       > $ git commit -m "Alteração arquivo 001" -m "Revisão da lógica A, B, C e afins" > $ git push origin main
