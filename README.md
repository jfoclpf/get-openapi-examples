## paths-openapi-yaml
### Get all paths present in openapi.yaml file based on paths and the provided examples

If a certain `openapi.yaml` file is like this example:

```yaml
paths:
  /district/{district}:
    get:
      operationId: getDistrict
      summary: Data of Distrito
      parameters:
        - in: path
          name: district
          required: true
          schema:
            type: string
          examples:
            porto:
              value: Porto
              summary: District of Porto
            lisbon:
              value: Lisbon
              summary: District of Lisbon

  /district/{district}/altimetry:
    get:
      operationId: getDistrictAltimetry
      summary: Altimetry of Distrito
      parameters:
        - in: path
          name: district
          required: true
          schema:
            type: string
            example: Porto
```

Then you use this module like this:

```js
const pathsOpenapiYaml = require('paths-openapi-yaml')
console.log(pathsOpenapiYaml('/path/to/openapi.yaml'))
/*
[
  '/district/Porto',
  '/district/Lisbon',
  '/district/Porto/altimetry'
}
*/

```
