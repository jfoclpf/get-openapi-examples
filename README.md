## paths-openapi-yaml
### Extract all possible paths present in `openapi.yaml` based on paths and the provided examples

This might be useful, for example, for testing routes. It supports different types of [examples](https://swagger.io/docs/specification/adding-examples/), and variables may be in the path or in the query.

If a certain `openapi.yaml` file is like this example:

```yaml
paths:
  /coordinates:
    get:
      operationId: getDataByCoordinates
      summary: Get data by Coordinates in query
      parameters:
        - in: query
          name: lat
          schema:
            type: string
            example: '40.153687'
          description: Latitude of the point
        - in: query
          name: lon
          schema:
            type: string
            example: '-8.514602'
          description: Longitude of the point

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
  '/coordinates?lat=40.153687&lon=-8.514602',
  '/district/Porto',
  '/district/Lisbon',
  '/district/Porto/altimetry'
}
*/

```
