# Integración Autenticación Moodle vía URL
Es un mecanismo de autenticación hacia una plataforma Moodle desde un Sistema Externo.
# Requerimientos
- Dirección IP Sistema Externo
# Uso
## Uso:
```
curl "https://dominio_plataforma_moodle/webservice/rest/server.php?wstoken=10101010101010010101&wsfunction=auth_userkey_request_login_url&moodlewsrestformat=json&user[username]=nombre_usuario"
```
El Token permite conversar el Sistema Externo con la plataforma Moodle, el usuario debe existir en Moodle.
#Referencia a las variables GET
La autenticación vía Moodle vía URL provee las siguientes variables a configurar:
|Nombre variable| Descripción| Valor
| ---            | ---                                                  |              |
| wstoken        | esto indica el token de autenticación                | alfanumérico |
| user[username] | esto indica el nombre de usuario existente en Moodle | alfanumérico |
