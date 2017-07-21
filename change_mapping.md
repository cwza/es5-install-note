# Rename index with A little down time for search

## Disable Input (Graceful shutdown)
queue all insert and update request at message queue

## Create Index
``` sh
curl -XPUT localhost:9200/meepshop_v2 -H 'Content-Type: application/json' -d '
{
    "settings":{
        "index.mapping.total_fields.limit": 6000,
        "number_of_replicas": 2
    },
    "mappings": {
    }
}'
```

## Reindex
``` sh
curl -XPOST localhost:9200/_reindex?pretty -d'{
  "source": {
    "index": "2910eb12_d64a_49cc_b2be_54201441e27b"
  },
  "dest": {
    "index": "meepshop_v2"
  }
}'
```

## Remove old index
``` sh
curl -XDELETE localhost:9200/2910eb12_d64a_49cc_b2be_54201441e27b
```

## Search Down Time

## Add Alias
``` sh
curl -XPOST localhost:9200/_aliases -H 'Content-Type: application/json' -d '
{
    "actions": [
        { "add": {
            "index": "meepshop_v2",
            "alias": "2910eb12_d64a_49cc_b2be_54201441e27b"
        }}
    ]
}'
```

## Enable Input

------------------------------

# Change mapping with zero down time

## Disable Input (Graceful shutdown)
queue all insert and update request at message queue

## Create Index
``` sh
curl -XPUT localhost:9200/meepshop_v3 -H 'Content-Type: application/json' -d '
{
    "settings":{
        "index.mapping.total_fields.limit": 6000,
        "number_of_replicas": 2
    },
    "mappings": {
    }
}'
```

## Reindex
``` sh
curl -XPOST localhost:9200/_reindex?pretty -d'{
  "source": {
    "index": "meepshop_v2"
  },
  "dest": {
    "index": "meepshop_v3"
  }
}'
```

## Add Alias
``` sh
curl -XPOST localhost:9200/_aliases -H 'Content-Type: application/json' -d '
{
    "actions": [
        { "remove": {
            "index": "meepshop_v2",
            "alias": "2910eb12_d64a_49cc_b2be_54201441e27b"
        }},
        { "add": {
            "index": "meepshop_v3",
            "alias": "2910eb12_d64a_49cc_b2be_54201441e27b"
        }}
    ]
}'
```

## Enable Input

## Remove Old Index
``` sh
curl -XDELETE localhost:9200/meepshop_v2
```
