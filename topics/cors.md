https://help.mulesoft.com/s/article/How-to-properly-configure-the-CORS-Interceptor-configuration-as-documented

The CORS Interceptor configuration as documented in https://docs.mulesoft.com/api-manager/2.x/cors-policy#configuring-cors-for-non-api-gateway-mule-environments is too generic, user needs more specific example on each element.
SOLUTION
Please note: Do not use the '*' wildcard in the Interceptor's origin url.

Here's a working example:
 

<http:listener-config name="HTTP_ODS" doc:name="HTTP Listener config" doc:id="dac36d1f-b722-47f4-889a-60faac32fdfb" basePath="/OrchUtilApi">
  <http:listener-connection host="0.0.0.0" port="9522" />
    <http:listener-interceptors>
      <http:cors-interceptor>
        <http:origins>
          <http:origin url="${internalapps.host}" accessControlMaxAge="10">
            <http:allowed-methods>
              <http:method methodName="POST"/>
              <http:method methodName="GET"/>
              <http:method methodName="OPTIONS"/>
              <http:method methodName="PUT"/>
              <http:method methodName="PATCH"/>
            </http:allowed-methods>
            <http:allowed-headers>
              <http:header headerName="Content-Type"/>
              <http:header headerName="Content-Length"/>
              <http:header headerName="Accept-Encoding"/>
              <http:header headerName="X-CSRF-Token"/>
              <http:header headerName="Authorization"/>
              <http:header headerName="Accept"/>
              <http:header headerName="origin"/>
              <http:header headerName="Cache-Control"/>
              <http:header headerName="X-Requested-With"/>
            </http:allowed-headers>
            <http:expose-headers>
              <http:header headerName="Content-Type"/>
              <http:header headerName="Content-Length"/>
              <http:header headerName="Authorization"/>
              <http:header headerName="X-Requested-With"/>
              <http:header headerName="Accept"/>
            </http:expose-headers>
          </http:origin>
        </http:origins>
      </http:cors-interceptor>
    </http:listener-interceptors>
  </http:listener-config>
</http:listener-config>
