# Autenticación hacia Moodle desde Sistema Externo usando URL
Es un mecanismo de autenticación hacia una plataforma Moodle desde un Sistema Externo.
# Requerimientos
- Dirección IP Sistema Externo
- Token
- URL Plataforma Moodle
- Usuario existente en Moodle
- cURL
# Uso
Autenticar a un alumno en Moodle desde un Sistema Externo tiene varios mecanismos, en este caso usaremos la conexión vía loginurl.
### Uso:
### Petición:
Usando la herramienta de linea de comandos cURL se realiza la petición
```
curl "https://DOMINIO_MOODLE/webservice/rest/server.php?wstoken=10101010101010010101&wsfunction=auth_userkey_request_login_url&moodlewsrestformat=json&user[username]=nombre_usuario"
```
El Token permite conversar el Sistema Externo con la plataforma Moodle.
- El usuario debe existir en Moodle.
# Referencia a las variables GET
La autenticación vía Moodle vía URL provee las siguientes variables a configurar:
| Nombre variable | Descripción                                          | Valor        |
| ---             | ---                                                  | ---          |
| DOMINIO_MOODLE  | Dominio dónde está implementada la plataforma        | URL          |
| wstoken         | esto indica el token de autenticación                | alfanumérico |
| user[username]  | esto indica el nombre de usuario existente en Moodle | alfanumérico |
- El dominio es proporcionado por PanalTech
- El Token es proporcionado por PanalTech
- El usuario es creado por PanalTech

### Respuesta:
Moodle retornará respuesta en esquema JSON con una URL y hash MD5
```
{"loginurl":"https:\/\/DOMINIO_MOODLE\/auth\/userkey\/login.php?key=MD5HASH"}
```
| Nombre variable | Descripción                    | Valor |
| ---             | ---                            | ---   |
| key             | Hash MD5 proveniente de Moodle | MD5   |
### Concatenar:
Se debe extraer todo el loginurl y concatenar las siguientes variables al final de la misma:
```
&wantsurl=DOMINIO_MOODLE/course/view.php?id=IDCURSO
```
| Nombre variable | Descripción                                              | Valor   |
| ---             | ---                                                      | ---     |
| wantsurl        | Dominio dónde está implementada la plataforma            | URL     |
| id              | Identificador del curso dónde está matriculado el alumno | Integer |
- id es proporcionado por PanalTech
### Redirigir
Con el loginurl concatenado se debe redirigir el alumno hacia la plataforma Moodle.
## Control de flujo y manejo de errores
## Error JSON
En caso exista un fallo en la ejecución del programa, se retornará el siguiente esquema JSON:
```
{"exception":"invalid_parameter_exception","errorcode":"invalidparameter","message":"Detectado valor de par\u00e1metro no v\u00e1lido"}
```
| Nombre variable | Descripción                                      | Valor  |
| ---             | ---                                              | ---    |
| exception       | Imprevisto ocurrido en la ejecución del programa | String |
| errorcode       | Identificación de la excepción detectada         | String |
| message         | Explicación del error                            | String |
## Creado por Servicios Informáticos PanalTech
Esta documentación fue desarrollada por PanalTech SpA.

https://www.panaltech.cl

![Screenshot](panaltech.png)
