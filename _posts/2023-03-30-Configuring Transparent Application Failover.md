How to Configuring Transparent Application Failover
--On primary 
$ srvctl add service -d $(srvctl config database) -s svc_tac -pdb PDB1 -role primary -replay_init_time 1000 -failoverretry 30 -failoverdelay 3 -commit_outcome TRUE -failovertype AUTO -failover_restore AUTO
$ srvctl start service -d $(srvctl config database) -s svc_tac
$ srvctl status service -d $(srvctl config database) -s svc_tac
$ srvctl config service -d $(srvctl config database) -s svc_tac
-- On the standby !!!
-- On the standby we don't start this service !!
[oracle@adgsby ~]$ srvctl add service -d $(srvctl config database) -s svc_tac -pdb PDB1 -role primary -replay_init_time 1000 -failoverretry 30 -failoverdelay 3 -commit_outcome TRUE -failovertype AUTO -failover_restore AUTO
[oracle@adgsby ~]$ srvctl status service -d $(srvctl config database) -s svc_tac
Service svc_tac is not running.
As this service is associated with the PRIMARY role of the database, don't start it on the standby database. The clusterware will do that automatically, should a switchover/failover occur.]

on your application level connecting to database through service name "svc_tac" .
