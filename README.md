# samples
Check the database failover ready satatus
select replica_id ,database_name ,is_failover_ready from sys.dm_hadr_database_replica_cluster_states

check the sysnc state
 SELECT 
  ar.replica_server_name,
  adc.database_name, 
  ag.name AS ag_name, 
  drs.is_local, 
  drs.is_primary_replica, 
  drs.synchronization_state_desc, 
  drs.is_commit_participant, 
  drs.synchronization_health_desc, 
  drs.recovery_lsn, 
  drs.truncation_lsn
FROM sys.dm_hadr_database_replica_states AS drs
INNER JOIN sys.availability_databases_cluster AS adc 
  ON drs.group_id = adc.group_id AND 
  drs.group_database_id = adc.group_database_id
INNER JOIN sys.availability_groups AS ag
  ON ag.group_id = drs.group_id
INNER JOIN sys.availability_replicas AS ar 
  ON drs.group_id = ar.group_id AND 
  drs.replica_id = ar.replica_id
ORDER BY 
  ag.name, 
  ar.replica_server_name, 
  adc.database_name;

 run on node to faiolver	
 ALTER AVAILABILITY GROUP AG1 FORCE_FAILOVER_ALLOW_DATA_LOSS;
 
 
 
 
 changes the permission if sqlserver giving error
 ls -laR /var/opt/mssql
chgrp -R 0 /var/opt/mssql
chmod -R g=u /var/opt/mssql
chown -R 10001:0 /var/opt/mssql
ls -laR /var/opt/mssql



misleniojus commands
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=PaSSw0rd' -p 14331:1433 -d enriquecatala/sql2017_alwayson_node:latest

SELECT * from Master . SYS . database_mirroring_endpoints

SELECT * from Master . SYS . Certificates

select * from sys.endpoints 

ALTER ENDPOINT Hadr_endpoint STATE = STOPPED 

ALTER ENDPOINT Hadr_endpoint STATE = STARTED
