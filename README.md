# SSL-ApacheTomcat
Some applications don't work correctly with security-constraint and want to push Http to Https This include simply bit different way to complete Http to Https Issue

**Generate your SSL Cetificates**

**Copy these files in to secured path in the server**

**Edit your server.xml File**

Located in apache-tomcat > conf > server.xml


`<Connector URIEncoding="UTF-8" port="80" acceptCount="100" enableLookups="false" maxThreads="150" redirectPort="443" />`

`<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <UpgradeProtocol className="org.apache.coyote.http2.Http2Protocol" />
        <SSLHostConfig>
            <Certificate certificateKeyFile="/usr/local/xxx/xxx.key"
                         certificateFile="/usr/local/xxx/xxx.crt"
                         certificateChainFile="/usr/local/xxx/xxx.crt"
                         type="RSA" />
        </SSLHostConfig>
</Connector>`

Add the following element into <Host name="localhost" ...> at last


`<Valve className="org.apache.catalina.valves.rewrite.RewriteValve" />`

**Edit you web.xml File** 

Located in apache-tomcat > conf > web.xml

To force Tomcat to redirect and revert all requested HTTP traffic over to HTTPS, configure the `conf/web.xml` file with the below block. 
This should be placed at the very end of the file near and above the ending `</webapp>` tag:


 `<security-constraint>
	<web-resource-collection>
	<web-resource-name>Protected Context</web-resource-name>
         <url-pattern>/*</url-pattern>
         <!--<url-pattern>/adportal/*</url-pattern>-->
	</web-resource-collection>
	<user-data-constraint>
	<transport-guarantee>CONFIDENTIAL</transport-guarantee>
	</user-data-constraint>
 </security-constraint>`


======Try restarting Apache-tomcat server========

Some applications don't work correctly with that security-constraint, so I followed a completely different approach:(It's Working on apache-tomcat 9)

**Create the file conf/Catalina/localhost/rewrite.config** 

Sample is attached with this


======Try restarting Apache-tomcat server again It should work ======

===================GOOD LUCK=================


