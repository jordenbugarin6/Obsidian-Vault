
```bash
** IN ORDER FOR ANY CHANGE TO OCCUR YOU MUST RESTART THE TEAMS SERVER **

Note:
Current Cobalt Strike build utilizes arsenal_kit-NO-AV-BYPASS.cna aggressor script by default and you must enable arsenal_kit-AV-BYPASS.cna.

# Enable AV Bypass
1. Open Cobalt Strike 
2. Navigate to Script Manager 
3. Unload /opt/cobaltstrike/arsenal-kit/dist/arsenal_kit-AV-BYPASS.cna 
4. Load /opt/cobaltstrike/arsenal-kit/dist/arsenal_kit-AV-BYPASS.cna
5. Restart Teams Server
6. Regenerate Payloads

# Disable AV Bypass (Default)
1. Open Cobalt Strike 
2. Navigate to Script Manager 
3. Unload /opt/cobaltstrike/arsenal-kit/dist/arsenal_kit-AV-BYPASS.cna 
4. Load /opt/cobaltstrike/arsenal-kit/dist/arsenal_kit-NO-AV-BYPASS.cna
5. Restart Teams Server
6. Regenerate Payloads

```