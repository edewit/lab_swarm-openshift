FROM registry.access.redhat.com/openshift3/nodejs-010-rhel7

ADD . /opt/app-root/src/

EXPOSE 8080

# The CMD. We do the following here:
#  - Process the env vars. All of them can be overriden at run time
#    so we need to run them through some logic on container bringup.
#  - Inject some env vars into the services.json.
#  - Inject some env vars into index.html
#  - Start the server via npm start.
CMD OLACHAINURL=${OLACHAINURL:-"http://ola-${OS_PROJECT}.${OS_SUBDOMAIN}/api/ola-chaining"} \
        HOLAURL=${HOLAURL:-"http://hola-${OS_PROJECT}.${OS_SUBDOMAIN}/api/hola"}           \
        BONJOURURL=${BONJOURURL:-"http://bonjour-${OS_PROJECT}.${OS_SUBDOMAIN}/api/bonjour"}  \
        ALOHAURL=${ALOHAURL:-"http://aloha-${OS_PROJECT}.${OS_SUBDOMAIN}/api/aloha"}        \
        OLAURL=${OLAURL:-"http://ola-${OS_PROJECT}.${OS_SUBDOMAIN}/api/ola"}              \
        APIGATEWAYURL=${APIGATEWAYURL:-"http://api-gateway-${OS_PROJECT}.${OS_SUBDOMAIN}/api"}   \
        HYSTRIXDASHBOARDURL=${HYSTRIXDASHBOARDURL:-"http://hystrix-dashboard-${OS_PROJECT}.${OS_SUBDOMAIN}"} \
        ZIPKINQUERYURL=${ZIPKINQUERYURL:-"http://zipkin-query-${OS_PROJECT}.${OS_SUBDOMAIN}"} \
    && sed -i.orig services.json \
        -e 's|OLACHAINURL|'"$OLACHAINURL"'|' \
        -e 's|HOLAURL|'"$HOLAURL"'|' \
        -e 's|BONJOURURL|'"$BONJOURURL"'|' \
        -e 's|ALOHAURL|'"$ALOHAURL"'|' \
        -e 's|OLAURL|'"$OLAURL"'|' \
        -e 's|APIGATEWAYURL|'"$APIGATEWAYURL"'|' \
    && sed -i.orig index.html \
        -e 's|HYSTRIXDASHBOARDURL|'"$HYSTRIXDASHBOARDURL"'|' \
        -e 's|ZIPKINQUERYURL|'"$ZIPKINQUERYURL"'|' \
    && /bin/bash -c 'npm start'
