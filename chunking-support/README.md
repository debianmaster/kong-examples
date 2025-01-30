```
curl -i -X POST http://localhost:8001/services \
  --data "name=streaming-service" \
  --data "url=http://upstream-service:port"

