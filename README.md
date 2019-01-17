# cas-server-webapp
1.基于数据库的cas 认证
2.本示例将已经将https关掉。如使用https自行打开


取消HTTPS协议方式

１．webapps\cas\WEB-INF\spring-configuration\warnCookieGenerator.xml 

修改  p:cookieSecure="true" 为 p:cookieSecure="false"
<bean id="warnCookieGenerator" class="org.jasig.cas.web.support.CookieRetrievingCookieGenerator"
        p:cookieSecure="false"
        p:cookieMaxAge="-1"
        p:cookieName="CASPRIVACY"
        p:cookiePath="/cas"/>

２．webapps\cas\WEB-INF\spring-configuration\ticketGrantingTicketCookieGenerator.xml ，修改  p:cookieSecure="true" 为 p:cookieSecure="false"

<bean id="ticketGrantingTicketCookieGenerator" class="org.jasig.cas.web.support.CookieRetrievingCookieGenerator"
        p:cookieSecure="false"
        p:cookieMaxAge="-1"
        p:cookieName="CASTGC"
        p:cookiePath="/cas"/>

３.修改webapps\cas\WEB-INF\deployerConfigContext.xml
<bean id="proxyAuthenticationHandler" 
class="org.jasig.cas.authentication.handler.support.HttpBasedServiceCredentialsAuthenticationHandler"
          p:httpClient-ref="httpClient"/>


增加p:requireSecure="false"即HTTPS为不采用。
修改后为：
  <bean id="proxyAuthenticationHandler"
class="org.jasig.cas.authentication.handler.support.HttpBasedServiceCredentialsAuthenticationHandler"
          p:httpClient-ref="httpClient" p:requireSecure="false"/>

