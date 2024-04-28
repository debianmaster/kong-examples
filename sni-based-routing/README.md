> Setup sni based routing
```
curl -X POST localhost:8001/certificates -F cert=@./example.com.crt -F key=@./example.com.key -F "snis[]=example.com"

echo "" | openssl s_client -connect 127.0.0.1 -port 8443 -servername example.com 2>/dev/null | openssl x509 -text -noout | head -10


curl -X POST localhost:8001/certificates -F cert=@./httpbin.org.crt -F key=@./httpbin.org.key -F "snis[]=httpbin.org"

echo "" | openssl s_client -connect 127.0.0.1 -port 8443 -servername httpbin.org 2>/dev/null | openssl x509 -text -noout | head -10



curl  -X POST localhost:8001/services \
  -F name=httpbin-svc \
  -F url=http://httpbin.org/anything

curl  -X POST localhost:8001/services/httpbin-svc/routes \
  -F name=httpbin-route \
  -F "paths[]=/" \
  -F "snis[]=httpbin.org"



curl  -X POST localhost:8001/services \
  -F name=example-svc \
  -F url=https://example.com

curl  -X POST localhost:8001/services/example-svc/routes \
  -F name=example-svc-route \
  -F "paths[]=/" \
  -F "snis[]=example.com"


curl -kv --resolve example.com:8443:127.0.0.1 https://example.com:8443


curl -kv --resolve httpbin.org:8443:127.0.0.1 https://httpbin.org:8443
```

