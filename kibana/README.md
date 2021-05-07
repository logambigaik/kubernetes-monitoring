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

'''
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
'''



