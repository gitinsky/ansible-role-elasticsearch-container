{{ elasticsearch_hosts }} is the name of ES hosts group, must be set.

##### Change number of replicas

If you have a single-node cluster you might want to change number of replicas to zero.

```bash
number_of_replicas=0
curl 127.0.0.1:9200/_cat/indices| while read health status index pri rep docs_count docs_deleted store_size pri_store_size
do
    if test "$number_of_replicas" != "$rep"
    then
        curl -XPUT "localhost:9200/$index/_settings" -d "{\"index\" : { \"number_of_replicas\" : $number_of_replicas }}"
    fi
done
```