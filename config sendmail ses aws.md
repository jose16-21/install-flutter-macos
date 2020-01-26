# Configuracion de Amazon SES con Sendmail

## Requisitos
- Tener instalado el paquete de sendmail.
- Tener instalado los siguientes paquetes: 
    `sendmail'cf`, `m4` y `cyrus-sasl-plain`
- tener un dominio o un correo electronico verficado como direccion remitente.

## Configurar Send mail
1. Con un editor de archivos desde la terminal ya sea `nano` o `vim` abrir el archivo `/etc/mail/authinfo`, si el archivo
   no existe se crea.

   `AuthInfo:email-smtp.us-west-2.amazonaws.com "U:root" "I:smtpUsername" "P:smtpPassword" "M:PLAIN"`

2. Escribir el siguiente comando para generar el archivo ` /etc/mail/authinfo.db`:

    `sudo sh -c 'makemap hash /etc/mail/authinfo.db < /etc/mail/authinfo'`

3. En la línea de comandos, escriba el siguiente comando para poder transmitir al punto de enlace SMTP de Amazon SES.

    `sudo sh -c 'echo "Connect:email-smtp.us-west-2.amazonaws.com RELAY" >> /etc/mail/access'`

4. En la línea de comandos, escriba el siguiente comando para volver a generar `/etc/mail/access.db`:

    `sudo sh -c 'makemap hash /etc/mail/access.db < /etc/mail/access'`

5. En la línea de comandos, escriba el siguiente comando para crear copias de seguridad de los archivos sendmail.mc y          sendmail.cf:

    `sudo sh -c 'cp /etc/mail/sendmail.cf /etc/mail/sendmail_cf.backup && cp /etc/mail/sendmail.mc /etc/mail/sendmail_mc.backup'`

6. Añadir las líneas siguientes al archivo /etc/mail/sendmail.mc delante de las definiciones de MAILER(), en example.com reemplazar con el nombre del dominio verificado.

```sh
define(`SMART_HOST', `email-smtp.us-west-2.amazonaws.com')dnl
define(`RELAY_MAILER_ARGS', `TCP $h 25')dnl
define(`confAUTH_MECHANISMS', `LOGIN PLAIN')dnl
FEATURE(`authinfo', `hash -o /etc/mail/authinfo.db')dnl
MASQUERADE_AS(`example.com')dnl
FEATURE(masquerade_envelope)dnl
FEATURE(masquerade_entire_domain)dnl
```
7. En la línea de comandos, escriba el siguiente comando para poder escribir en *sendmail.cf*:

`sudo chmod 666 /etc/mail/sendmail.cf`

8. En la línea de comandos, escriba el siguiente comando para volver a generar *sendmail.cf*:

`sudo sh -c 'm4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf'`

9. En la línea de comandos, escriba el siguiente comando para restablecer los permisos de *sendmail.cf* a solo lectura:

`sudo chmod 644 /etc/mail/sendmail.cf` 

si tenera error instalar el siguiete `yum -y install sendmail-cf`

10. En la línea de comandos, escriba el siguiente comando para reiniciar Sendmail:

`sudo /etc/init.d/sendmail restart`

11. Siga los pasos que se describen a continuación para enviar un correo electrónico de prueba:

- En la línea de comandos, escriba el comando siguiente:

`/usr/sbin/sendmail -vf sender@example.com recipient@example.com`

- Escriba el siguiente contenido del mensaje. Pulse Enter al final de cada línea.

```sh
From: sender@example.com
To: recipient@example.com
Subject: Amazon SES test email
This is a test message sent from Amazon SES using Sendmail.
```
al terminar de escribir el contenido de correo electronico, pulsar **Ctr+D** para enviarlo o finalizando el proceso con un **.**

12.  Compruebe el cliente de correo electrónico del destinatario para el correo electrónico. Si no puede encontrar el correo electrónico, busque en la carpeta de correo no deseado. Si continúa sin poder encontrar el correo electrónico, consulte el registro de Sendmail en su servidor de correo electrónico. El registro se encuentra normalmente en */var/log/mail.log*.
