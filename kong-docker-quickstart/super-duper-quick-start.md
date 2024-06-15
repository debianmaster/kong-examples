```
export KONG_LICENSE_DATA=''
```

```
curl -Ls https://get.konghq.com/quickstart | PROXY_PORT=80 bash -s --  -t 3.4 -m \
    -e KONG_PASSWORD=changeme \
    -e KONG_ADMIN_GUI_URL=http://manager.kong.zelarsoft.com \
    -e KONG_ADMIN_GUI_API_URL=http://admin.kong.zelarsoft.com \
    -e KONG_PORTAL_GUI_PROTOCOL=http \
    -e KONG_PORTAL_API_URL=http://portalapi.kong.zelarsoft.com \
    -e KONG_PORTAL_GUI_HOST=portal.kong.zelarsoft.com \
    -e KONG_PORTAL="on" \
    -e "KONG_ADMIN_GUI_AUTH=basic-auth" \
    -e KONG_ENFORCE_RBAC="on" \
    -e KONG_LICENSE_DATA \
    -e "KONG_ADMIN_GUI_SESSION_CONF={\"secret\":\"Y29vbGJlYW5z\",\"cookie_samesite\":\"off\",\"cookie_domain\": \".kong.zelarsoft.com\"}" \
    -e KONG_PORTAL_SESSION_CONF='{"cookie_name": "portal_session", "secret": "PORTAL_SUPER_SECRET", "storage": "kong", "cookie_secure": false, "cookie_domain":".kong.zelarsoft.com"}'
    

curl -X POST localhost:8001/services -d name=admin -d url=http://localhost:8001 -H "Kong-Admin-Token: changeme"
curl -X POST localhost:8001/services -d name=manager -d url=http://localhost:8002 -H "Kong-Admin-Token: changeme"
curl -X POST localhost:8001/services -d name=portal -d url=http://localhost:8003 -H "Kong-Admin-Token: changeme"
curl -X POST localhost:8001/services -d name=portalapi -d url=http://localhost:8004 -H "Kong-Admin-Token: changeme"
curl -X POST localhost:8001/services/admin/routes -d hosts=admin.kong.zelarsoft.com -H "Kong-Admin-Token: changeme"
curl -X POST localhost:8001/services/manager/routes -d hosts=manager.kong.zelarsoft.com -H "Kong-Admin-Token: changeme"
curl -X POST localhost:8001/services/portal/routes -d hosts=portal.kong.zelarsoft.com -H "Kong-Admin-Token: changeme"
curl -X POST localhost:8001/services/portalapi/routes -d hosts=portalapi.kong.zelarsoft.com -H "Kong-Admin-Token: changeme"
```
