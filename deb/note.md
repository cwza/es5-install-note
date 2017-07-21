## mappings
### Deprecated only warning
1. {"type": "string", "index": "not_analyzed"} => {"type": "keyword", "index": true}
2. {"type": "string"} => {"type": "text"} 

### mapping change
1. process_date from date to string, and TradeDate from date to string
2. 
``` json
PUT 2910eb12_d64a_49cc_b2be_54201441e27b/
{
    "settings":{
        "index.mapping.total_fields.limit": 6000,
        "number_of_replicas": 2
    },
    "mappings":{

    }
}
```

## query change
filter => post_filter

## refs
change mapping table names
```
orderRegular => orderregular
fbStore => fbstore
storeApp => storeapp
orderLog => orderlog
appCategory => appcategory
storeShipment => storeshipment
ioLog => iolog
cronJob => cronjob
order => orders
memberGroup => membergroup
exportFormat => exportformat
userPoints => userpoints
orderApply => orderapply
user => users
orderProduct => orderproduct
wishList => wishlist
webTrack => webtrack
appLogin => applogin
orderCache => ordercache
initVersion => initversion
storePayment => storepayment
```
cart2, service, happy, 