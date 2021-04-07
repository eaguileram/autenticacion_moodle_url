# Integración Autenticación Moodle vía URL
Es un mecanismo de autenticación hacia una plataforma Moodle desde un Sistema Externo.
# Requerimientos
- Dirección IP Sistema Externo
# Uso
## Uso:
```
curl "https://dominio_plataforma_moodle/webservice/rest/server.php?wstoken=10101010101010010101&wsfunction=auth_userkey_request_login_url&moodlewsrestformat=json&user[username]=nombre_usuario"
```
El Token permite conversar con la plataforma Moodle y el usuario debe existir en la misma.
