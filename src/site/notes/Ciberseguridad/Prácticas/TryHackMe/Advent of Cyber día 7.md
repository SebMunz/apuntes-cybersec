---
{"dg-publish":true,"permalink":"/Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 7/"}
---

[[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 6\|Advent of Cyber día 6]]

Conocimientos:
- AWS
	- Cloudwatch
	- Cloudtrail
- JQ

---

En este ejercicio vamos a revisar logs en AWS, a través de CloudWatch, para investigar qué sucedió con los dineros del servicio.

# Cloudwatch
Es una plataforma de monitoreo y observabilidad que nos ayuda a investigar el entorno AWS. Monitorea métricas, configura alarmas, etc.
Se debe instalar un agente en la instancia para que la captura de métricas sea exitosa.

Tres términos importantes:
- Log event:
	- una entrada o evento. tiene estampa de tiempo y el mensaje + metadata
- Log streams:
	- una colección de logs de una sola fuente
- Log groups:
	- colección de log streams. Lo realiza cuando tiene lógica hacerlo, como el mismo servicio en varios hosts.

## CloudTrail
CloudWatch puede hacerle un seguimiento a la infraestructura y el performance de aplicaciones. Pero para monitorear acciones en el entorno AWS, utilizamos CloudTrail. Cada acción que un usuario toma (a través de la consola) o servicio, se captura y se guarda.
- Siempre activo
- Formato JSON
- Historial de eventos (90 días)
- Trails
	- se pueden definir trails propios para capturar acciones específicas para monitorear escenarios y guardarlos por más de 90 días, por ejemplo
- Enviable
	- Se permite configurar los logs de cloudtrail para que lleguen a cloudwatch

Todo esto podemos aplicarlo a servicios como S3 o IAM.

---
# JQ
JQ es un procesador de linea de comandos que se puede usar con JSON de manera similar a `sed`, `awk`y `grep`.

JQ recibe dos inputs: el filtro que usaremos + el archivo que leeremos.

Comenzamos el filtro JQ con un `.`, que le dice a JQ que vamos a acceder la entrada actual. De ahí, queremos acceder a los valores JSON guardados en array `[]`, osea, tendriamos algo así:
`jq '.[]' book_list.json`
o podriamos profundizar, agregando una llave del json:
`jq '.[] | .book_title' book_list.json`

A grandes rasgos, nos ayuda a hacer más fácil la lectura, filtrado y acceso de archivos json.

--- 

# Investigación

La narrativa del desafío nos cuenta a grandes rasgos:
- Care4wares levantó una caridad
- 28 de noviembre se mandó un enlace con un folleto que tenía detalles de la caridad.
- detalles como el número de cuenta
- primer día recibieron donaciones
- segundo día no recibieron
- preguntando a la gente, si se habían hecho donaciones pero no se recibieron.
- el número de transacción estaba incorrecto.
- El link es el mismo, pero tiene otro número de cuenta.
- el folleto, `wareville-bank-account-qr.png` se guardó un bucket S3 llamado `wareville-care4wares`

Un log usualmente se ve así:
```json
{
  "eventVersion": "1.10",
  "userIdentity": {
    "type": "IAMUser",
    "principalId": "AIDAXRMKYT5O5Y2GLD4ZG",
    "arn": "arn:aws:iam::518371450717:user/wareville_collector",
    "accountId": "518371450717",
    "accessKeyId": "AKIAXRMKYT5OZCZPGNZ7",
    "userName": "wareville_collector"
  },
  "eventTime": "2024-10-21T22:13:24Z",
  "eventSource": "s3.amazonaws.com",
  "eventName": "ListObjects",
  "awsRegion": "ap-southeast-1",
  "sourceIPAddress": "34.247.218.56",
  "userAgent": "[aws-sdk-go/0.24.0 (go1.22.6; linux; amd64)]",
  "requestParameters": {
    "bucketName": "aoc-cloudtrail-wareville",
    "Host": "aoc-cloudtrail-wareville.s3.ap-southeast-1.amazonaws.com",
    "prefix": ""
  },
  "responseElements": null,
  "additionalEventData": {
    "SignatureVersion": "SigV4",
    "CipherSuite": "TLS_AES_128_GCM_SHA256",
    "bytesTransferredIn": 0,
    "AuthenticationMethod": "AuthHeader",
    "x-amz-id-2": "yqniVtqBrL0jNyGlvnYeR3BvJJPlXdgxvjAwwWhTt9dLMbhgZugkhlH8H21Oo5kNLiq8vg5vLoj3BNl9LPEAqN5iHpKpZ1hVynQi7qrIDk0=",
    "bytesTransferredOut": 236375
  },
  "requestID": "YKEKJP7QX32B4NZB",
  "eventID": "fd80529f-d0af-4f44-8034-743d8d92bdcf",
  "readOnly": true,
  "resources": [
    {
      "type": "AWS::S3::Object",
      "ARNPrefix": "arn:aws:s3:::aoc-cloudtrail-wareville/"
    },
    {
      "accountId": "518371450717",
      "type": "AWS::S3::Bucket",
      "ARN": "arn:aws:s3:::aoc-cloudtrail-wareville"
    }
  ],
  "eventType": "AwsApiCall",
  "managementEvent": false,
  "recipientAccountId": "518371450717",
  "eventCategory": "Data",
  "tlsDetails": {
    "tlsVersion": "TLSv1.3",
    "cipherSuite": "TLS_AES_128_GCM_SHA256",
    "clientProvidedHostHeader": "aoc-cloudtrail-wareville.s3.ap-southeast-1.amazonaws.com"
  }
}
```

Puede ser un poco intenso de primera vista pero es todo descriptivo.
En lo que nos podemos enfocar ahora mismo:

| Campo             | Descripción                                                     |
| ----------------- | --------------------------------------------------------------- |
| userIdentity      | Detalles de la cuenta de usuario que actuó sobre un objeto      |
| eventTime         | Cuándo ocurrio                                                  |
| eventType         | Qué tipo de evento ocurrió (AwsApiCall ? AwsConsoleSignIn ?)    |
| eventSource       | Desde dónde se logeo este evento                                |
| eventName         | Qué acción específica ocurrió (ListObjects ? GetBucketObject ?) |
| sourceIPAddress   | Desde dónde vino la acción                                      |
| userAgent         | Que agente de usuario lo realizó (Firefox ? AWS CLI ?)          |
| requestParameters | Qué parámetros estuvieron involucrados (BucketName ?)           |
Osea, en nuestro log podemos ver:
- el usuario IAM, `wareville_collector`, listó los objetos (ListObjects event) del S3 llamado `aoc-cloudtrail-wareville`
- `34.247.218.56` o la IP desde dónde se originó
- El user agent que usó `AWS SDK tool for Go`

Usemos JQ para filtrar logs de eventos relacionados con el objeto S3 `wareville-bank-account-qr.png`

A través de la consola navegamos a `wareville_logs` y utilizamos el siguiente comando:
`jq -r '.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName=="wareville-care4wares") | [.eventTime, .eventName, .userIdentity.userName // "N/A",.requestParameters.bucketName // "N/A", .requestParameters.key // "N/A", .sourceIPAddress // "N/A"]' cloudtrail_log.json`

Se ve complejo pero no lo es, la estructura sigue siendo la misma:
- -r es una bandera para que nos entregue los resultados en json duro
- el resto es simplemente pedirle parámetros específicos, filtros, etc
- `// "N/A"` básicamente le dice que si no encuentra el valor anteriormente mencionado, coloque "N/A"
- `| @tsv` separa los valores procesado después del filtro como valores separados por tab (tab separated values)
- `| column ...` recibe todo el output (que esta en tsv) y lo embellece alineando columnas.

Con esto obtenemos el siguiente resultado:
![](https://i.imgur.com/U7cCege.png)

Básicamente nos dice que tenemos 5 eventos relacionados con el bucket `wareville-care4wares`, todos relacionados al usuario `glitch`. Listó los objetos del bucket pero también subió un archivo: `wareville-bank-account-qr.png` que coincide con la fecha. Es un usuario anómalo.

Ahora, podríamos investigar todos los eventos relacionados con este usuario:
![](https://i.imgur.com/hmFgYrQ.png)
Lo más relevante es que ingresó a la consola (`ConsoleLogin`), lo que nos dice que se usó la cuenta para acceder a la consola de AWS en un navegador.

![](https://i.imgur.com/BnvRxcL.png)
Podemos deducir que tilizó una máquina MacOS con Chrome.

Ahora, podríamos buscar quién creo la cuenta. Filtremos los eventos relacionados a IAM.
![](https://i.imgur.com/VI2AdVm.png)

Con esto ya podemos ir entendiendo para donde va el asunto.
Básicamente a través de filtrados de logs vamos encontrando quién creo esa cuenta anómala pero deberiamos verificar los eventos relacionados a esa IP maliciosa y si esta IP ha accedido otras cuentas.

Lo que encontramos es lo siguiente:
- el incidente tuvo un acceso anómalo con el usuario `mcskidy`desde la IP `53.94.201.69`
- se creó una cuenta, `glitch`
- a `glitch` se le asignaron permisos de admin
- `glitch` accedió al S3 `wareville-care4wares`, reemplazó el archivo del folleto. La IP usada para acceder a las cuentas y al User-Agent, es la misma en todos los casos
- sin embargo, el User-Agent string y la IP de donde recurrentemente se accede a la cuenta de `mcskidy`es distinta a la usada ahora.

Lo que ahora podriamos hacer es buscar en los logs de RDS.
Con el comando `grep` filtramos el query `INSERT INTO`:
`grep "INSERT INTO" rds.log`
![](https://i.imgur.com/EWyvZPR.png)

Y nos encontramos con lo que necesitabamos.

---

# Preguntas

Para responder las preguntas simplemente debemos utilizar los comandos de filtro para jq.
Las dos preguntas sobre IP las podemos deducir a través de los mismos logs.
La última pregunta la respondemos con el comando grep!

Con eso concluimos el día 7
![](https://i.imgur.com/qF2LmmW.png)

Procedamos al [[Ciberseguridad/Prácticas/TryHackMe/Advent of Cyber día 8\|Advent of Cyber día 8]]