# Autenticación hacia Moodle desde Sistema Externo usando LoginURL
Es un mecanismo de autenticación hacia una plataforma Moodle desde un Sistema Externo.
# Requerimientos
- Informar Dirección IP para habilitación
- Token de Acceso provisto por PanalTech
- URL Plataforma Aula Virtual
- Usuarios existentes
# Uso
Autenticar a un alumno en Moodle desde un Sistema Externo tiene varios mecanismos, en este caso usaremos la integración vía loginurl.
### Uso:
### Petición:
Se debe realizar una petición POST a la siguiente URL
```
https://DOMINIO_AULA/webservice/rest/server.php?wstoken=10101010101010010101&wsfunction=auth_userkey_request_login_url&moodlewsrestformat=json&user[username]=nombre_usuario
```
El Token permite conversar el Sistema Externo con la plataforma Moodle.
- El usuario debe existir en Moodle.
# Referencia a las variables GET
La autenticación hacia Moodle vía URL provee las siguientes variables a configurar:
| Nombre variable | Descripción                                          | Valor        |
| ---             | ---                                                  | ---          |
| DOMINIO_AULA    | Dominio dónde está implementada la plataforma        | URL          |
| wstoken         | esto indica el token de autenticación                | alfanumérico |
| user[username]  | esto indica el nombre de usuario existente en Moodle | alfanumérico |
- El dominio es proporcionado por PanalTech
- El Token es proporcionado por PanalTech
- El usuario es creado por PanalTech

### Respuesta:
Moodle retornará una respuesta en esquema JSON con una URL y hash MD5
```
{"loginurl":"https:\/\/DOMINIO_AULA\/auth\/userkey\/login.php?key=HASH_ACCESO"}
```
| Nombre variable | Descripción                    | Valor  |
| ---             | ---                            | ---    |
| key             | Hash de acceso                 | String |
- El Hash de acceso tiene una duración de 5 minutos, luego de eso expira y debe solicitarse nuevamente.
### Armar URL para redirigir usuario:
Se debe concatenar el "loginurl" de la respuesta a la petición anterior con la siguiente variable al final de la misma:
```
&wantsurl=URLREQUERIDA
```
| Nombre variable | Descripción                                              | Valor   |
| ---             | ---                                                      | ---     |
| wantsurl        | URL a la que se desea acceder                            | URL     |

- URL de curso tiene el formato:
```
https://DOMINIO_AULA/course/view.php?id=IDCURSO
```
- DOMINIO_AULA es el dominio de la plataforma virtual a la que se accede
- IDCURSO es proporcionado por PanalTech

Quedando como sigue:

```
https://DOMINIO_AULA/auth/userkey/login.php?key=HASH_ACCESO&wantsurl=https://DOMINIO_AULA/course/view.php?id=IDCURSO
```

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
## Creado por PanalTech SpA
Esta documentación fue desarrollada por PanalTech SpA.

https://www.panaltech.cl

![Screenshot](panaltech.png)
