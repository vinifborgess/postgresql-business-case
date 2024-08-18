# postgresql-business-case
Business case using PostgreSQL, MS PowerBI w/ PowerQuery.


## Introdução

Projeto de análise de dados que visa a restauração de um arquivo .sql usando 'Restore' do PostgreSQL, pelo método do Query Tool. Gerenciamento de dados utilizando PowerQuery conectando diretamente no servidor do PostgreSQL.
Analytics final entregue usando MS PowerBi.


## Instalação

- Antes de iniciar, certifique-se que você possui o PostgreSQL instalado em sua máquina. 
- Caso você tenha esquecido suas credenciais, clique no tutorial a seguir: [tutorial de recuperação de senha].
- Disponibilização do arquivo (.sql) [link do zip];


## Step 1: Restauração do arquivo

Setup do PostgreSQL: dentro do ambiente do PostgreSQL, verifique a versão do seu aplicativo. Você pode verificar de diversas formas, a mais fácil e segura é conectando-se no banco de dados genérico gerado 'postgres', clique com o botão direito em Query Tool, insira suas credenciais (caso não saiba ou tenha perdido, acesse aqui). Com o terminal aberto, digite ```SELECT version();``` a saída do comando incluirá informações seguras sobre a versão do PostgreSQL.

Essa etapa é crucial, pois é quando você instala o PostgreSQL em seu sistema, esses utilitários são instalados em um diretório específico. No entanto, se você tiver mais de uma versão do PostgreSQL instalada em seu sistema, pode haver diretórios diferentes para cada versão.

Portanto, o PostgreSQL precisa saber onde encontrar esses utilitários para que você possa usá-los. Isso é feito definindo os caminhos binários corretos para cada versão do PostgreSQL. Os caminhos binários são as localizações dos diretórios onde os utilitários estão instalados.

Ao definir os caminhos binários corretos, você garante que o PostgreSQL use a versão correta dos utilitários para a versão do banco de dados que você está usando. Isso é importante porque cada versão do PostgreSQL pode ter alterações ou melhorias nos utilitários, e usar a versão incorreta pode resultar em comportamentos inesperados ou erros.

## Step 1.1: Ajustando os caminhos binários

No PostgreSQL, vá em Files -> Preferences -> Binary Paths -> e ajuste com o caminho do diretório onde o PostgreSQL, em sua máquina, está instalado.

Por exemplo, o diretório C:\Program Files\PostgreSQL\16\bin é o diretório onde os utilitários do PostgreSQL 16 estão instalados. Se você tiver instalado o PostgreSQL 16 em seu sistema, você deve definir o caminho binário para esse diretório nas lacunas em aberto na seção do EDB Advanced Server Binary Path e PostgreSQL Binary Path.

Ajuste o caminho de acordo com a versão de seu PostgreSQL.

## Step 1.2: Migração do código SQL em .txt para o PostgreSQL

Com os caminhos binários ajustados, vá no fonte de dados (.sql), abra ela com o editor de texto de sua preferência. Com a abertura do código, dê um CTRL + A para copiar todo o código e um CTRL + C para encaminhá-lo à sua área de transferência. 

Vá à base de dados 'postgres' ou à alguma de sua preferência, clique com o botão direito acima do nome da base, abra o Query Tool e cole o código copiado em sua área de transferência. Ou seja, migre o código SQL do arquivo-fonte para o terminal.

## Step 2: Execução e Validação

Com o botão F5, execute a consulta. Após a run, as tabelas do código (6) foram geradas com sucesso, de maneira lógica e segura, dentro de 'Schemas', na sua base de dados selecionada.

As tabelas geradas foram:
- x
- y
- n
- l
- m
- z

Para visualização e checagem, dentro de 'Schemas' -> public -> Tables -> verifique se as seis tabelas do código SQL foram geradas. Para melhor entendimento dos dados, com o botão direito, clique em View/Edit Data para visualizar o dataset.

## Step 3: Ingestão dos dados no ambiente do MS PowerBI

O MS PowerBI, por sua vez, possui conexão integrada com o SGBD do projeto (PostgreSQL). Em Obter Dados, pesquise por PostgreSQL e selecione a opção 'Banco de dados PostgreSQL'. 

Como o projeto está sendo executado em ambiente local, na aba de servidor, digite o seu localhost (localhost ou 127.0.0.1) e a base de dados onde as tabelas estão hospedadas.

## Step 4: Importação e Data Management

Importe todas as tabelas para o PowerQuery, ambiente de gerenciamento de dados nativo do MS PowerBI.


