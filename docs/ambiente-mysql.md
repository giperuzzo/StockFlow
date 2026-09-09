Entendendo a instalação e configuração do MySQL no StockFlow

1. O que eu já tinha instalado

No início, eu já tinha uma instalação do MySQL no computador.

Também já possuía o MySQL Workbench, que é a ferramenta gráfica utilizada para acessar e administrar o banco de dados.

É importante entender que MySQL Server e MySQL Workbench são coisas diferentes:

* MySQL Server: é o servidor responsável por executar e armazenar os bancos de dados.
* MySQL Workbench: é uma ferramenta gráfica utilizada para se conectar ao servidor e trabalhar com os bancos.

⸻

2. Instalação do MySQL Server 26.7

Durante a configuração do ambiente, foi instalado o:

MySQL Server 26.7

Ele criou um serviço no Windows chamado:

MySQL267

Esse serviço é responsável por manter o servidor MySQL funcionando em segundo plano.

Durante os testes, identificamos que essa instalação estava utilizando a porta:

3307

Portanto:

MySQL Server 26.7
        ↓
Serviço: MySQL267
        ↓
Porta: 3307

⸻

3. O problema inicial com a senha

Quando tentei acessar o servidor pelo MySQL Workbench, não lembrava a senha do usuário root.

A primeira mensagem apresentada foi:

Access denied for user 'root'@'localhost'

Isso significava que o servidor estava sendo encontrado, mas a autenticação do usuário root não estava sendo aceita.

Foi necessário redefinir a senha do usuário root.

Para isso, foi utilizado temporariamente um arquivo de inicialização:

mysql-init.txt

Depois de redefinir a senha e confirmar que o acesso funcionava pelo terminal, o arquivo foi excluído, pois continha a senha em texto puro.

⸻

4. O problema de compatibilidade

Depois de resolver a senha, surgiu outro problema.

O MySQL Workbench que estava instalado era:

MySQL Workbench 8.0.34

Enquanto o servidor instalado era:

MySQL Server 26.7

Ao tentar realizar a conexão, apareceu uma mensagem semelhante a:

Incompatible protocol detected

Isso não significava que a senha estava errada.

O problema estava relacionado à compatibilidade entre o MySQL Workbench 8.0.x e o MySQL Server 26.7.

⸻

5. Atualização do MySQL Workbench

Para tentar melhorar a compatibilidade, o Workbench foi atualizado de:

8.0.34

para:

8.0.47

Mesmo assim, ao tentar conectar ao MySQL Server 26.7, o Workbench continuou apresentando um aviso de compatibilidade.

Isso mostrou que o problema não era simplesmente uma versão antiga do Workbench.

A combinação:

Workbench 8.0.x
        +
MySQL Server 26.7

não era a melhor combinação para o ambiente que eu estava montando.

⸻

6. Instalação do MySQL Server 8.4

Para trabalhar com uma versão mais adequada ao ambiente do Workbench, foi instalado também o:

MySQL Server 8.4.11

Essa instalação foi feita como uma side-by-side installation, ou seja, sem substituir o MySQL Server 26.7.

Para evitar conflito entre os dois servidores, cada um utiliza uma porta diferente.

Servidores instalados

Servidor	Serviço Windows	Porta
MySQL 26.7	MySQL267	3307
MySQL 8.4.11	MySQL84	3308

Assim, os dois servidores podem coexistir no mesmo computador.

⸻

7. Por que usamos a porta 3308?

A porta 3306 é uma porta tradicionalmente utilizada pelo MySQL.

Porém, durante a configuração do MySQL 8.4, a porta 3306 apareceu como ocupada.

Como o MySQL 26.7 estava utilizando a porta 3307, foi escolhida a porta:

3308

Dessa forma:

127.0.0.1:3307 → MySQL Server 26.7
127.0.0.1:3308 → MySQL Server 8.4.11

⸻

8. Configuração do MySQL 8.4

Durante a configuração do MySQL Server 8.4 foram definidos:

* Tipo de computador: Development Computer
* Protocolo: TCP/IP
* Porta: 3308
* Usuário administrativo: root
* Serviço do Windows: MySQL84
* Inicialização automática do serviço: ativada
* Conta do serviço: Standard System Account
* Instalação lado a lado: ativada
* Bancos de exemplo: não instalados

⸻

9. Criação da conexão no Workbench

No MySQL Workbench 8.0.47 foi criada uma nova conexão chamada:

StockFlow 8.4

Configuração:

Connection Name: StockFlow 8.4
Hostname: 127.0.0.1
Port: 3308
Username: root

Ao testar a conexão, o Workbench apresentou novamente um aviso relacionado à compatibilidade com o servidor 8.4.

Foi escolhida a opção de continuar mesmo assim.

Depois disso, apareceu:

Successfully made the MySQL connection

Isso confirmou que o Workbench conseguiu se conectar ao:

MySQL Server 8.4.11

através da porta:

3308

⸻

10. O que realmente aconteceu?

O problema não foi simplesmente “o Workbench estava com defeito”.

O que aconteceu foi uma sequência de situações diferentes:

Primeiro problema

Eu não lembrava a senha do root.

Solução: redefinir a senha.

Segundo problema

O Workbench 8.0.34 apresentou incompatibilidade ao tentar trabalhar com o MySQL Server 26.7.

Solução inicial: atualizar o Workbench para 8.0.47.

Terceiro problema

Mesmo com o Workbench atualizado, a combinação com o MySQL Server 26.7 continuou apresentando avisos de compatibilidade.

Solução adotada: instalar o MySQL Server 8.4.11 separadamente.

Resultado

Agora tenho um ambiente funcionando com:

MySQL Workbench 8.0.47
             ↓
     StockFlow 8.4
             ↓
       127.0.0.1
             ↓
          Porta 3308
             ↓
     MySQL Server 8.4.11

⸻

11. O que aprendi com essa configuração?

Essa configuração ajudou a entender alguns conceitos importantes de banco de dados e infraestrutura:

* diferença entre MySQL Server e MySQL Workbench;
* conceito de cliente e servidor;
* usuário e autenticação;
* usuário root;
* senha do banco;
* serviço do Windows;
* host;
* 127.0.0.1 (localhost);
* portas de comunicação;
* múltiplas instâncias do MySQL;
* instalação side-by-side;
* compatibilidade entre versões de cliente e servidor.

⸻

12. Próximo passo do StockFlow

Com o MySQL Server 8.4.11 funcionando e o Workbench conectado, o próximo passo será criar o banco de dados do projeto:

stockflow

Antes de criar as tabelas, será importante entender a diferença entre:

* servidor;
* database/schema;
* tabela;
* registro;
* coluna.

Depois disso, o modelo que foi desenvolvido na documentação do StockFlow poderá começar a ser transformado em tabelas reais no MySQL.

A ideia não é apenas executar comandos prontos, mas entender como o modelo conceitual e o modelo lógico do StockFlow se transformam em um banco de dados funcional.