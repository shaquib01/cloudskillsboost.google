# ENABLE APIs
>Database Migration API

>Service Networking API

## Task 1 
>Go TO VM INSTANCE > CLICK ON SSH
```
sudo apt install postgresql-13-pglogical
sudo su - postgres -c "gsutil cp gs://cloud-training/gsp918/pg_hba_append.conf ."
sudo su - postgres -c "gsutil cp gs://cloud-training/gsp918/postgresql_append.conf ."
sudo su - postgres -c "cat pg_hba_append.conf >> /etc/postgresql/13/main/pg_hba.conf"
sudo su - postgres -c "cat postgresql_append.conf >> /etc/postgresql/13/main/postgresql.conf"

sudo systemctl restart postgresql@13-main
sudo su - postgres
psql
\c postgres;
CREATE EXTENSION pglogical;
\c orders;
CREATE EXTENSION pglogical;
\c gmemegen_db;
CREATE EXTENSION pglogical;
\l
CREATE USER migration_admin PASSWORD 'DMS_1s_cool!';
ALTER DATABASE orders OWNER TO migration_admin;
ALTER ROLE migration_admin WITH REPLICATION;
\c postgres;
GRANT USAGE ON SCHEMA pglogical TO migration_admin;
GRANT ALL ON SCHEMA pglogical TO migration_admin;

GRANT SELECT ON pglogical.tables TO migration_admin;
GRANT SELECT ON pglogical.depend TO migration_admin;
GRANT SELECT ON pglogical.local_node TO migration_admin;
GRANT SELECT ON pglogical.local_sync_status TO migration_admin;
GRANT SELECT ON pglogical.node TO migration_admin;
GRANT SELECT ON pglogical.node_interface TO migration_admin;
GRANT SELECT ON pglogical.queue TO migration_admin;
GRANT SELECT ON pglogical.replication_set TO migration_admin;
GRANT SELECT ON pglogical.replication_set_seq TO migration_admin;
GRANT SELECT ON pglogical.replication_set_table TO migration_admin;
GRANT SELECT ON pglogical.sequence_state TO migration_admin;
GRANT SELECT ON pglogical.subscription TO migration_admin;
\c orders;
GRANT USAGE ON SCHEMA pglogical TO migration_admin;
GRANT ALL ON SCHEMA pglogical TO migration_admin;

GRANT SELECT ON pglogical.tables TO migration_admin;
GRANT SELECT ON pglogical.depend TO migration_admin;
GRANT SELECT ON pglogical.local_node TO migration_admin;
GRANT SELECT ON pglogical.local_sync_status TO migration_admin;
GRANT SELECT ON pglogical.node TO migration_admin;
GRANT SELECT ON pglogical.node_interface TO migration_admin;
GRANT SELECT ON pglogical.queue TO migration_admin;
GRANT SELECT ON pglogical.replication_set TO migration_admin;
GRANT SELECT ON pglogical.replication_set_seq TO migration_admin;
GRANT SELECT ON pglogical.replication_set_table TO migration_admin;
GRANT SELECT ON pglogical.sequence_state TO migration_admin;
GRANT SELECT ON pglogical.subscription TO migration_admin;
GRANT USAGE ON SCHEMA public TO migration_admin;
GRANT ALL ON SCHEMA public TO migration_admin;

GRANT SELECT ON public.distribution_centers TO migration_admin;
GRANT SELECT ON public.inventory_items TO migration_admin;
GRANT SELECT ON public.order_items TO migration_admin;
GRANT SELECT ON public.products TO migration_admin;
GRANT SELECT ON public.users TO migration_admin;
\c gmemegen_db;
GRANT USAGE ON SCHEMA pglogical TO migration_admin;
GRANT ALL ON SCHEMA pglogical TO migration_admin;

GRANT SELECT ON pglogical.tables TO migration_admin;
GRANT SELECT ON pglogical.depend TO migration_admin;
GRANT SELECT ON pglogical.local_node TO migration_admin;
GRANT SELECT ON pglogical.local_sync_status TO migration_admin;
GRANT SELECT ON pglogical.node TO migration_admin;
GRANT SELECT ON pglogical.node_interface TO migration_admin;
GRANT SELECT ON pglogical.queue TO migration_admin;
GRANT SELECT ON pglogical.replication_set TO migration_admin;
GRANT SELECT ON pglogical.replication_set_seq TO migration_admin;
GRANT SELECT ON pglogical.replication_set_table TO migration_admin;
GRANT SELECT ON pglogical.sequence_state TO migration_admin;
GRANT SELECT ON pglogical.subscription TO migration_admin;
GRANT USAGE ON SCHEMA public TO migration_admin;
GRANT ALL ON SCHEMA public TO migration_admin;

GRANT SELECT ON public.meme TO migration_admin;

\c orders;
\dt
ALTER TABLE public.distribution_centers OWNER TO migration_admin;
ALTER TABLE public.inventory_items OWNER TO migration_admin;
ALTER TABLE public.order_items OWNER TO migration_admin;
ALTER TABLE public.products OWNER TO migration_admin;
ALTER TABLE public.users OWNER TO migration_admin;
\dt
\q
exit
```

## TASK 2
> click Database Migration > Connection profiles.

> Click + Create Profile.

>For Database engine, select PostgreSQL

>For Connection profile name, enter postgres-vm

>FOR IP GO TO VM INSTANCE AND COPY INTERNAL IP 

>For Port, enter 5432.
>For Username, enter
```
migration_admin.
```

>For Password,
```
enter DMS_1s_cool!
```

>For Region select >us-west1.

> For all other values leave the defaults.

Click Create.
##  Task 3. Create and start a continuous migration job

>click Database Migration > Migration jobs.

>Click + Create Migration Job.

>For Migration job name, enter 
```
vm-to-cloudsql
```
>For Source database engine, select PostgreSQL.

>For Destination region, select >us-west1.(CHECK OWN)

>For Destination database engine, select Cloud SQL for PostgreSQL.

>For Migration job type, select Continuous.

>Leave the defaults for the other settings.

>Click Save & Continue.

>Destination Instance ID, enter
```postgresql-cloudsql
```

For Password, 
```
supersecret!.
```

>For Choose a Cloud SQL edition, select >Enterprise edition.
>For Database version >select Cloud SQL for PostgreSQL 13.

>For Instance connectivity, select >Private IP and >Public IP.

>Select Use an automatically allocated IP range.

>Leave the defaults for the other settings.

>Allocate & Connect.
>For Machine shapes. check 1 vCPU, 3.75 GB

>For Storage type, select SSD >select 10 GB >Create & Continue.
>VPC peering >Configure & Continue.

## Task 4. Confirm the data in Cloud SQL for PostgreSQL
```
export VM_NAME=postgresql-vm
export PROJECT_ID=$(gcloud config list --format 'value(core.project)')
export POSTGRESQL_IP=$(gcloud compute instances describe ${VM_NAME} \
  --zone=us-west1-c --format="value(networkInterfaces[0].accessConfigs[0].natIP)")
echo $POSTGRESQL_IP
psql -h $POSTGRESQL_IP -p 5432 -d orders -U migration_admin
```
```
DMS_1s_cool!
```
```
\c orders;
insert into distribution_centers values(-80.1918,25.7617,'Miami FL',11);
\q
```
```
gcloud sql connect postgresql-cloudsql --user=postgres --quiet
```
```
supersecret!
```
```
\c orders;
```
```
supersecret!
```
```
select * from distribution_centers;
```

# TASK 5 JUST WAIT TO CLICK PROMOTE OPTION 
