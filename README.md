# sql-server-tutorial


1- Instale o sql-server seguindo este link -> https://docs.microsoft.com/pt-br/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-2017<br>

2- Para restaurar um backup sql-server no ubuntu siga estes passos.<br>
   Primeiramente se conecte no terminal de edição sql-server já instalado, com o comando<br> -> 'sqlcmd -S localhost -U SA' (insira a senha logo em seguida).<br>
   Use este comando para saber quais são os arquivos que você deve restaurar.<br>
      RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'<br>
      GO<br>
        
        exemplo: RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/BD/fisio/fisio_backup_2019_07_26_081001_3947299.bak
        tem como retorno os arquivos 
        -> fisio (Nome Lógico) e fisio.mdf (Nome físico)
        -> fisio_readonly (Nome Lógico) e fisio_readonly.mdf (Nome físico)
        -> fisio_log (Nome Lógico) e fisio_log.mdf (Nome físico)
        
   Execute estes comandos para iniciar a restauração dos arquivo obtidos com o comando 2.2.1<br>
       RESTORE DATABASE YourDB<br>
       FROM DISK = '/var/opt/mssql/backup/YourDB.bak'<br>
       WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',<br>
       MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'<br>
       GO<br>
        
        exemplo: RESTORE DATABASE fisio
                 FROM DISK = '/var/opt/mssql/backup/BD/fisio/fisio_backup_2019_07_26_081001_3947299.bak'
                 WITH MOVE 'YourDB' TO '/var/opt/mssql/data/fisio.mdf',
                 MOVE 'fisio_readonly' TO '/var/opt/mssql/data/fisio_readonly.ndf',
                 MOVE 'fisio_log' TO '/var/opt/mssql/data/fisio_log.ldf'
                 GO
        
  
<p>Ao fim destes passos você já está apto a se conectar junto ao banco e listar suas informações,
    use este comando abaixo para saber quais databases você possui:
    SELECT Name FROM sys.Databases
    GO </p>


**Uteis**<br>
Para listar todas tabelas existentes em sua base utilize o comando<br> -> ```SELECT table_catalog, table_schema, table_name, table_type FROM information_schema.tables```
<br>Para iniciar, reiniciar ou parar o servidor SQL-SERVER use estes comandos<br> -> ```sudo systemctl stop mssql-server```
 ->```sudo systemctl start mssql-server```<br>
 ->```sudo systemctl restart mssql-server```<br>
