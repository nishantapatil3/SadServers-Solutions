

# Solution
```
docker ps -a and docker logs envoy

# cluster name is incorrect, fix it to 'express_cluster'

# add below config to /etc/admin/envoy.yaml
- name: express_cluster
  ...
  common_lb_config:
    healthy_panic_threshold:
      value: 0

docker restart envoy
```