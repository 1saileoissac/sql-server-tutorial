# sql-server-tutorial


1- Instale o sql-server seguindo este link -> https://docs.microsoft.com/pt-br/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-2017

2- Para restaurar um backup sql-server no ubuntu siga estes passos.
   2.1- Primeiramente se conecte no terminal de edição sql-server já instalado, com o comando -> 'sqlcmd -S localhost -U SA' (insira a senha logo em seguida).
   2.2- Use este comando para saber quais são os arquivos que você deve restaurar.
        2.2.1- RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
        2.2.2- GO
        
   2.3- Execute estes comandos para iniciar a restauração dos arquivo obtidos com o comando 2.2.1
        2.3.1- RESTORE DATABASE YourDB
        2.3.2- FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
        2.3.3- WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
        2.3.4- MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
        2.3.5- GO
      
        Ao fim destes passos você já está apto a se conectar junto ao banco e listar suas informações
        Use este comando abaixo para saber quais databases você possui:
        SELECT Name FROM sys.Databases
        GO













**Uteis**
Para listar todas tabelas existentes em sua base utilize o comando -> ```sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD```
