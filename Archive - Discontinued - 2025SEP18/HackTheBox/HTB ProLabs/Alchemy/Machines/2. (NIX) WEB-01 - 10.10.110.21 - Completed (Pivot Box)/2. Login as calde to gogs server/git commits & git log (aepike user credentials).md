# git commit browsing method
When browsing the commits once logged in as `calde_ldap` (alot of scrolling) you come across a commit from `aepike` user, when clicking the commit you come across the credentials for the `aepike` user
![[Pasted image 20240613113733.png]]
clicking on the `cfd2757dc8` commit shows the credentials for `aepike`
![[Pasted image 20240613113819.png]]
# git log method
once the interested repository is cloned utilize `git log -p` and hit `spacebar` to browse and eventually you will find the password
```bash
┌──(root💀gobots)-[13Jun2024 15:38:36]-[/home/kali/SUT/Alchemy/BreweryControlSystem-ST]
└─# git log -p     
```
![[Pasted image 20240613113141.png]]

```bash
commit cfd2757dc8f5f6c9fd423305bb4b84c91b24fb02
Author: Amalabairga Epiktetos <aepike@alchemy.htb>
Date:   Wed Nov 1 08:26:50 2023 -0400

    Access control documentation

diff --git a/access_control.st b/access_control.st
index 6e01c9b..671edd0 100644
--- a/access_control.st
+++ b/access_control.st
@@ -1,6 +1,6 @@
 PROGRAM AccessControl
 VAR
-  Password: STRING(16) := "LandIAtErOUs";  (* password *)
+  Password: STRING(16) := "password_here";  (* Set your own password *)
   EnteredPassword: STRING(16);


```