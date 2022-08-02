# es

## 某个用户绑定的所有手表型号
```
GET nginx-access-europe-prod-api-europe-2021.09/_search
{
  "size": 0,
  "aggs": {
    "uuid_terms": { // add uuid cardinality
      "terms": {
        "field": "uuid.keyword"
      },
      "aggs": {
        "bluetooth_name_terms": {
          "terms": {
            "field": "bluetooth_name.keyword",
            "size": 20 // save cardinality value to check the uuid had how many connects
          }
        },
        "bluetooth_name_cardinality": {
          "cardinality": {
            "field": "bluetooth_name.keyword"
          }
        }
      }
    }
  }
}
```

## 某个用户绑定的所有手表型号(带query除去无用uuid, 但效率低排除)
```
GET nginx-access-europe-prod-api-europe-2021.09/_search
{
  "size": 0,
  "query": {
    "bool": {
      "filter": {
        "script": {
          "script": {
            "source": "doc['uuid.keyword'].toString().length() > 10"
          }
        }
      }
    }
  },
  "aggs": {
    "uuid_terms": {
      "terms": {
        "field": "uuid.keyword"
      },
      "aggs": {
        "bluetooth_name_terms": {
          "terms": {
            "field": "bluetooth_name.keyword"
            "size": 20
          }
        },
        "bluetooth_name_cardinality": {
          "cardinality": {
            "field": "bluetooth_name.keyword"
          }
        }
      }
    }
  }
}
```

## 某一适配号的手表有哪些用户使用
```
GET nginx-access-europe-prod-api-europe-2021.09/_search
{
  "size": 0,
  "aggs": {
    "bluetooth_adapter_terms": {
      "terms": {
        "field": "bluetooth_adapter.keyword"
      },
      "aggs": {
        "uuid_terms": {
          "terms": {
            "field": "uuid.keyword"
          }
        },
        "uuid_cardinality": {
          "cardinality": {
            "field": "uuid.keyword"
          }
        }
      }
    },
    "bluetooth_adapter_cardinality": {
      "cardinality": {
        "field": "bluetooth_adapter.keyword"
      }
    }
  }
}
```

## 某一型号的手表有哪些用户使用
```
GET nginx-access-europe-prod-api-europe-2021.09/_search
{
  "size": 0,
  "aggs": {
    "bluetooth_name_terms": {
      "terms": {
        "field": "bluetooth_name.keyword"
      },
      "aggs": {
        "uuid_terms": {
          "terms": {
            "field": "uuid.keyword"
          }
        },
        "uuid_cardinality": {
          "cardinality": {
            "field": "uuid.keyword"
          }
        }
      }
    },
    "bluetooth_name_cardinality": {
      "cardinality": {
        "field": "bluetooth_name.keyword"
      }
    }
  }
}
```

## es 7.x fielddata
```
PUT nginx-access-europe-prod-api*/_mapping
{
  "properties": {
    "http_user_agent": {
      "type": "text",
      "fielddata": true
    }
  }
}
```
