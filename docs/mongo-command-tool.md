# Mongo command line tool

## Continue after created takiwa-mongo folder 
```
docker run --name takiwa-mongo -v ~/Takiwa/takiwa-mongo:/data/db -v ~/Takiwa/mongo-backup:/data/mongo-backup -p 27017:27017 -d mongo:4.0-xenial
```

```
sudo docker start takiwa-mongo
```
## mongodump and mongorestore 
### Mongo restore
```
docker exec -i takiwa-mongo sh -c 'mongorestore --db takiwaWarehouse /data/mongo-backup/takiwaWarehouse'
```

`mongorestore --db takiwaWarehouse /data/mongo-backup/takiwaWarehouse`

`mongodump --db takiwaWarehouse -c CollectionName -o /data/mongo-backup`

### run shell or mongo shell in docker
How to start **shell** for mongodump

```
docker exec -i takiwa-mongo sh
```
How to start a **mongodb shell** in docker container?

```
docker exec -it mongoContainer(takiwa-mongo) mongo
```

## mongoexport and mongoimport

### Export example.  
also can use  --skip 200 --limit 100 --sort '{a: 1}'
```
mongoexport --db takiwaWarehouse --collection dataset_structures -q '{createdAt: { $gt: { "$date": "2020-10-05T22:00:00.000Z" } } }' --out /data/mongo-backup/dataset_structures.json
```

### Import example. 
also may need --legacy
```
mongoimport --db takiwaWarehouse -c dataset_structures  --mode upsert --file /data/mongo-backup/dataset_structures.json
```
```
mongoimport --db takiwaWarehouse -c containers --mode upsert --file /data/mongo-backup/containers.json --jsonArray
```

###  Restore Example.  
copy collection to another collection purpose
```
mongorestore --db takiwaWarehouse -c geodata_CENSUS_NZ_2018_SA2_Clipped_GFERL9 --dir=/data/mongo-backup/takiwaWarehouse/geodata_CENSUS_NZ_2018_SA2_GFERL9.bson
```

### Create compound index example
    db.geodata_CENSUS_NZ_2018_SA2_GFERL9.createIndex({
        ageGroupId : 1,
        ethnicGroupId : 1,
        highestQualificationId: 1,
        sexId: 1,
        yearId: 1
    }, { name: 'filterQueryIndex', background: true })