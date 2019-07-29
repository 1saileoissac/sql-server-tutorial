# sql-server-tutorial


1- Instale o sql-server seguindo este link -> https://docs.microsoft.com/pt-br/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-2017<br>

2- Para restaurar um backup sql-server no ubuntu siga estes passos.<br>
   2.1- Primeiramente se conecte no terminal de edição sql-server já instalado, com o comando -> 'sqlcmd -S localhost -U SA' (insira a senha logo em seguida).<br>
   2.2- Use este comando para saber quais são os arquivos que você deve restaurar.<br>
        2.2.1- RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'<br>
        2.2.2- GO<br>
        
        exemplo: RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/BD/fisio/fisio_backup_2019_07_26_081001_3947299.bak
        tem como retorno os arquivos <br> -> fisio (Nome Lógico) e fisio.mdf (Nome físico)
        
   2.3- Execute estes comandos para iniciar a restauração dos arquivo obtidos com o comando 2.2.1<br>
        2.3.1- RESTORE DATABASE YourDB<br>
        2.3.2- FROM DISK = '/var/opt/mssql/backup/YourDB.bak'<br>
        2.3.3- WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',<br>
        2.3.4- MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'<br>
        2.3.5- GO<br>
        
        exemplo: RESTORE DATABASE fisio <br>
                 FROM DISK = '/var/opt/mssql/backup/BD/fisio/fisio_backup_2019_07_26_081001_3947299.bak' <br>
                 WITH MOVE 'YourDB' TO '/var/opt/mssql/data/fisio.mdf', <br>
                 MOVE 'fisio_readonly' TO '/var/opt/mssql/data/fisio_readonly.ndf', <br>
                 MOVE 'fisio_log' TO '/var/opt/mssql/data/fisio_log.ldf' <br>
                 GO <br>
        
  
>Ao fim destes passos você já está apto a se conectar junto ao banco e listar suas informações,
    use este comando abaixo para saber quais databases você possui:
    SELECT Name FROM sys.Databases
    GO.


**Uteis**<br>
Para listar todas tabelas existentes em sua base utilize o comando<br> -> ```SELECT table_catalog, table_schema, table_name, table_type FROM information_schema.tables```
<br>Para iniciar, reiniciar ou parar o servidor SQL-SERVER use estes comandos<br> -> ```sudo systemctl stop mssql-server```
 ->```sudo systemctl start mssql-server```<br>
 ->```sudo systemctl restart mssql-server```<br>
