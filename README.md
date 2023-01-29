# 2023-Team-Theta
This is the repository for Team Theta's Hackathon project that was held on January 28th & 29th at the 2023 Summit at the Wynn Hotel in Las Vegas, Nevada.

Github Actions leveraging Acumatica's REST API released for [2022 R2](https://help-2022r2.acumatica.com/(W(1))/Wiki/Show.aspx?pageid=7eddb850-0096-41c3-8ea7-14becf6401ff) to build and publish customizations from source for CI/CD integration.

## REST API
### Login

https://{{baseUrl}}/entity/auth/login

```json
{
    "name": "{{name}}",
    "password": "{{password}}",
    "company": "{{company}}",
    "branch": "{{branch}}"
}
```

### Import

https://{{baseUrl}}/CustomizationApi/Import
```json
{
    "projectLevel": 1,
    "isReplaceIfExists": true,
    "projectName": "ThetaHackathon",
    "projectDescription": "Customization Project for Team Theta",
    "projectContentBase64": "UEsDBBQAAAAIAHaHOFaekXSEuWEAAB6BAAALAAAA ..."
}
```

### Check Project Validation
Set the isOnlyValidation flag to true to check if the customization is valid

https://{{baseUrl}}/CustomizationApi/publishBegin

```json
{
    "isMergeWithExistingPackages": false,
    "isOnlyValidation": true,
    "isOnlyDbUpdates": false,
    "isReplayPreviouslyExecutedScripts": false,
    "projectNames": [ "ThetaHackathon" ],
    "tenantMode": "Current"
}
```

### Publish Customization
Set the isOnlyValidation flag to false to publish the customization to production

https://{{baseUrl}}/CustomizationApi/publishBegin

```json
{
    "isMergeWithExistingPackages": false,
    "isOnlyValidation": false,
    "isOnlyDbUpdates": false,
    "isReplayPreviouslyExecutedScripts": false,
    "projectNames": [ "ThetaHackathon" ],
    "tenantMode": "Current"
}
```

To check the status of a validation or publication, use publishEnd endpoint.  You may need to check periodically every 30 seconds to see if the isComplete flag is true. <br />
https://hackathon.acumatica.com/Theta/CustomizationApi/publishEnd
