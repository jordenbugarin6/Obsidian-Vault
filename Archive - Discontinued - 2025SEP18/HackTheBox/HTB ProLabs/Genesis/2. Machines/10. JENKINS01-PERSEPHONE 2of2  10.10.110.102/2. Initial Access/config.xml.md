```bash
lucian@JENKINS01-Persephone:~/.jenkins/users/admin$ cat config.xml
cat config.xml
<?xml version='1.0' encoding='UTF-8'?>
<user>
  <fullName>admin</fullName>
  <properties>
    <jenkins.security.ApiTokenProperty>
      <apiToken>{AQAAABAAAAAwYIS3SS+UHmUnr6MqszW9zKt5FyscIxP8Tsn6EBd+jkTU7AMGjfX71QjdHYF/uryF1DwtBEmVp+ARonWDAc+a3g==}</apiToken>
    </jenkins.security.ApiTokenProperty>
    <hudson.model.MyViewsProperty>
      <views>
        <hudson.model.AllView>
          <owner class="hudson.model.MyViewsProperty" reference="../../.."/>
          <name>all</name>
          <filterExecutors>false</filterExecutors>
          <filterQueue>false</filterQueue>
          <properties class="hudson.model.View$PropertyList"/>
        </hudson.model.AllView>
      </views>
    </hudson.model.MyViewsProperty>
    <hudson.model.PaneStatusProperties>
      <collapsed/>
    </hudson.model.PaneStatusProperties>
    <hudson.search.UserSearchProperty>
      <insensitiveSearch>true</insensitiveSearch>
    </hudson.search.UserSearchProperty>
    <hudson.security.HudsonPrivateSecurityRealm_-Details>
      <passwordHash>#jbcrypt:$2a$10$Mun8VB4BPhDiVpAPcTg08OOF8Sse1lr7TPF1PIIm8A54x.z722Zmy</passwordHash>
    </hudson.security.HudsonPrivateSecurityRealm_-Details>
    <jenkins.security.LastGrantedAuthoritiesProperty>
      <roles>
        <string>authenticated</string>
      </roles>
      <timestamp>1609796527011</timestamp>
    </jenkins.security.LastGrantedAuthoritiesProperty>
  </properties>
</user>lucian@JENKINS01-Persephone:~/.jenkins/users/admin$ 

```