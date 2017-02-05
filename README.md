# swgapi-spec
Define API I/F using swagger specifications

# API Design Workflow
  1) the API will be defined using swagger specifications. learn about it on http://swagger.io/specification/

  2) update swagger.yml to include the new API specification. refer to following example
```yaml
---
swagger: '2.0'
info:
  version: 0.9.0
  title: Simple Hello World Greeting Example
  description: A sample API to demonstrate features in the swagger-2.0 specification
paths:
  /greeting:
    get:
      description: returns a greeting to the user and a count on how many times the API greeted since start of service
      produces:
        - application/json
      parameters:
        - name: name
          in: query
          description: name of user to greet
          required: false
          type: string
      responses:
        '200':
          description: greeting response
          schema:
            $ref: '#/definitions/greeting'
        default:
          description: unexpected error
          schema:
            $ref: '#/definitions/errorModel'
definitions:
  greeting:
    type: object
    required:
      - id
      - content
    properties:
      id:
        type: integer
        format: int64
      content:
        type: string
  errorModel:
    type: object
    required:
      - code
      - message
    properties:
      code:
        type: integer
        format: int32
      message:
        type: string
```

  3) verify yaml
```bash
TBD
```

  4) generate server files

    * using the cli jar file
```bash
java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate \
  -i swagger.yaml \
  -l spring \
  -o out/server/swgapi
```

    * using docker
```bash
docker run -it \
    -v $PWD/out/server:/swagger-api/out \
    -v $PWD:/swagger-api/yaml \
    jimschubert/swagger-codegen-cli generate \
    -i /swagger-api/yaml/swagger.yml \
    -l spring \
    -o /swagger-api/out/swgapi
```

  5) generate sdk files
```bash
TBD
```

  6) push generated files to repo
```bash
TBD
```

# Tools
