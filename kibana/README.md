#  Elasticsearch.io
               Link : https://cloud.elastic.co/deployments/103eedca4b354bd286f47c5d182f50ac

![image](https://user-images.githubusercontent.com/54719289/117513825-764c6d80-af8a-11eb-93ff-41c1b82eabe3.png)

![image](https://user-images.githubusercontent.com/54719289/117513874-8ebc8800-af8a-11eb-8549-639e850de774.png)


Username: elastic and password : 2ZPHE99WTlojotbx2M4jG5Py(after reset password is :


![image](https://user-images.githubusercontent.com/54719289/117514031-de02b880-af8a-11eb-8d0d-540a0c740ecb.png)


# Launch kibana
![image](https://user-images.githubusercontent.com/54719289/117514382-96306100-af8b-11eb-880a-d3c68e4c27f0.png)


# Explore on my own:
![image](https://user-images.githubusercontent.com/54719289/117514351-81ec6400-af8b-11eb-913c-459d7610fb15.png)



# Console:  --> CLick Dev tools for editor
![image](https://user-images.githubusercontent.com/54719289/117514610-266ea600-af8c-11eb-96dc-d7f99be02a27.png)
![image](https://user-images.githubusercontent.com/54719289/117514640-3be3d000-af8c-11eb-90b3-5530d1fc58b6.png)


# GET _cluster/health:

![image](https://user-images.githubusercontent.com/54719289/117514935-f2e04b80-af8c-11eb-8cb6-419641ed8251.png)


#  SEARCH query;

            GET _search
            {
              "query": {
                  "match_all": {}
                  }
            }

![image](https://user-images.githubusercontent.com/54719289/117515227-86198100-af8d-11eb-8ea3-dd36cd0a95cc.png)


# Loading data for testing( Adding index template for testing):

https://github.com/logambigaik/data-visualization-with-kibana/blob/master/adding-index-templates.md      

```
PUT /_template/access-logs
{
  "index_patterns": ["access-logs*"],
  "settings": {
    "index.mapping.coerce": false
  }, 
  "mappings": {
    "dynamic": false,
    "properties": {
      "@timestamp": { "type": "date" },
      "message": { "type": "text" },
      "event.dataset": { "type": "keyword" },
      "hour_of_day": { "type": "short" },
      "http.request.method": { "type": "keyword" },
      "http.request.referrer": { "type": "keyword" },
      "http.response.body.bytes": { "type": "long" },
      "http.response.status_code": { "type": "long" },
      "http.version": { "type": "keyword" },
      "url.fragment": { "type": "keyword" },
      "url.path": { "type": "keyword" },
      "url.query": { "type": "keyword" },
      "url.scheme": { "type": "keyword" },
      "url.username": { "type": "keyword" },
      "url.original": {
        "type": "keyword",
        "fields": {
          "text": {
            "type": "text",
            "norms": false
          }
        }
      },
      "client.address": { "type": "keyword" },
      "client.ip": { "type": "ip" },
      "client.geo.city_name": { "type": "keyword" },
      "client.geo.continent_name": { "type": "keyword" },
      "client.geo.country_iso_code": { "type": "keyword" },
      "client.geo.country_name": { "type": "keyword" },
      "client.geo.location": { "type": "geo_point" },
      "client.geo.region_iso_code": { "type": "keyword" },
      "client.geo.region_name": { "type": "keyword" },
      "user_agent.device.name": { "type": "keyword" },
      "user_agent.name": { "type": "keyword" },
      "user_agent.version": { "type": "keyword" },
      "user_agent.original": {
        "type": "keyword",
        "fields": {
          "text": {
            "type": "text",
            "norms": false
          }
        }
      },
      "user_agent.os.version": { "type": "keyword" },
      "user_agent.os.name": {
        "type": "keyword",
        "fields": {
          "text": {
            "type": "text",
            "norms": false
          }
        }
      },
      "user_agent.os.full": {
        "type": "keyword",
        "fields": {
          "text": {
            "type": "text",
            "norms": false
          }
        }
      }
    }
  }
}
```

# After adding index:


![image](https://user-images.githubusercontent.com/54719289/117516029-ce39a300-af8f-11eb-8fa8-8e104411d42a.png)




## Index pattern for orders dataset
```
PUT /_template/orders
{
  "index_patterns": ["orders*"],
  "settings": {
    "index.mapping.coerce": false
  }, 
  "mappings": {
    "dynamic": false,
    "properties": {
      "@timestamp": { "type": "date" },
      "id": { "type": "keyword" },
      "product": {
        "properties": {
          "id": { "type": "keyword" },
          "name": { "type": "keyword" },
          "price": { "type": "float" },
          "brand": { "type": "keyword" },
          "category": { "type": "keyword" }
        }
      },
      "customer.id": { "type": "keyword" },
      "customer.age": { "type": "short" },
      "customer.gender": { "type": "keyword" },
      "customer.name": { "type": "keyword" },
      "customer.email": { "type": "keyword" },
      "channel": { "type": "keyword" },
      "store": { "type": "keyword" },
      "salesman.id": { "type": "keyword" },
      "salesman.name": { "type": "keyword" },
      "discount": { "type": "float" },
      "total": { "type": "float" }
    }
  }
}
```

# After that run the index template for dataset:

![image](https://user-images.githubusercontent.com/54719289/117516135-1e186a00-af90-11eb-90ed-3df3a2b8e5a1.png)


# Importing test data:

![image](https://user-images.githubusercontent.com/54719289/117516284-97b05800-af90-11eb-961a-6ff89b36447b.png)


# Test data:
[TestData](https://github.com/logambigaik/data-visualization-with-kibana/blob/master/test-data.zip)


# Install elasticsearch in cloudsystem and update pport 9200:
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.9.3-x86_64.rpm
rpm -ivh elasticsearch-7.9.3-x86_64.rpm

```

Open "elasticsearch.yml" and edit below details

vi /etc/elasticsearch/elasticsearch.yml

--------------------------------------------------
  network.host: 0.0.0.0
  http.port: 9200
  discovery.type: single-node
--------------------------------------------------
Start the service

service elasticsearch start
Check status of Elastic Search
service elasticsearch status

![image](https://user-images.githubusercontent.com/54719289/117538060-5190de00-affc-11eb-86bd-f7b33cff49bf.png)

# Kibana SetUp
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.9.3-x86_64.rpm
rpm -ivh kibana-7.9.3-x86_64.rpm
```
# Open "kibana.yml" and edit below details
```
vi /etc/kibana/kibana.yml
--------------------------------------------------
  server.port: 5601
  server.host: "0.0.0.0"
  elasticsearch.hosts: ["http://localhost:9200"]
--------------------------------------------------

```

# Start the service

service kibana start
Check status of Elastic Search

service kibana status

# Loading Data into cloud server command:
```
cd test-data

curl -H "Content-Type: application/x-ndjson" -u elastic:2ZPHE99WTlojotbx2M4jG5Py -XPOST http://35.178.188.146:9200/_bulk --data-binary "@orders.bulk.ndjson"
curl -H "Content-Type: application/x-ndjson" -u elastic:2ZPHE99WTlojotbx2M4jG5Py -XPOST http://35.178.188.146:9200/_bulk --data-binary "@nginx-access-logs-2020-01.bulk.ndjson"
curl -H "Content-Type: application/x-ndjson" -u elastic:2ZPHE99WTlojotbx2M4jG5Py -XPOST http://35.178.188.146:9200/_bulk --data-binary "@nginx-access-logs-2020-02.bulk.ndjson"
(curl-commnd)                                             (username:password)                       (cloud server)                                  (filename)          

'''


# Now, we have logs for 3 days :



# For creating index for each logs:

Click Stack management:
![image](https://user-images.githubusercontent.com/54719289/117539081-d7168d00-b000-11eb-81da-8aa7b35a393b.png)

Click Index Patterns:
![image](https://user-images.githubusercontent.com/54719289/117539137-28268100-b001-11eb-90c0-7f8a217a0599.png)
![image](https://user-images.githubusercontent.com/54719289/117539150-48564000-b001-11eb-8b91-625814842494.png)



  

