# Carbon Terra

Esta herramienta ha sido desarrollada para facilitar la configuración de las herramientas de AWS y desplegar tus aplicaciones. Después de ejecutar `npm run start`, verás la siguiente pantalla:

![image](https://github.com/BlackstoneStudio/Blackstone-Code-Standards/assets/26130533/65f3706b-8fc0-4311-a945-dcd28650547b)


## Opciones Disponibles

A continuación, se describen cada una de las opciones y sus parámetros necesarios:

### Amazon S3

Servicio de almacenamiento basado en la nube.

- **Bucket Name** (Requerido): Identificador para tu almacenamiento.

### Amazon CloudFront

Servicio web que agiliza la distribución de contenido web estático y dinámico como archivos .html, .css, .js y archivos de imágenes a los usuarios.

- **Domain name** (Requerido): URL proporcionada por el servicio Amazon S3 (omite https://).
- **CNAME**: Dominio personalizado para tu servicio CloudFront, esto requiere agregar un certificado ARN.
- **Certificado ARN**: ARN del certificado generado en Certificate Manager.

### AWS Certificate Manager (ACM)

Permite manejar la complejidad de crear, almacenar y renovar certificados y claves SSL/TLS públicos y privados.

- **Domain Name** (Requerido): URL en la que se implementará el certificado.
- **Validate Type** (Email or DNS): Esto será para verificar el dominio en su gestor DNS.

### Amazon Elastic Container Registry (ECR)

Almacenamiento y administración de imágenes de Docker.

- Para esta ejecución es necesario crear un archivo Docker a nivel de `/src`.
- **Upload image to an existing repository?** - Y / N. Si la opción es Y, el sistema solicitará la URL del repositorio (Repository Uri).
- **Repository Name**: Nombre que se asignará.
- **Repository Uri**: URL del repositorio existente al que se enviará la imagen de Docker.
- **Tag Name**: Identificador para la imagen a subir (ej: prod, dev).
- **Send Image** - Y/N. Si la opción es N, solo se creará el repositorio sin subir ninguna imagen de Docker.

### AWS App Runner

Servicio de aplicaciones en contenedores completamente administrado que permite crear, implementar y ejecutar servicios de API y aplicaciones web en contenedores sin experiencia previa en contenedores o infraestructuras.

- **Service Name**: Nombre que se asignará (debe ser único).
- **Image Url**: URL de una imagen existente de ECR.
- **Access Role ARN**: Rol de IAM que otorga al servicio App Runner acceso a un repositorio de origen (ejemplo: `arn:aws:iam::372527289275:role/service-role/AppRunnerECRAccessRole`).
- **Image Port**: Puerto para el App Runner (por defecto: 8080).

### Amazon Route 53

Servicio web de sistema de nombres de dominio (DNS) escalable y de alta disponibilidad.

- **Created records in an existing hosted zone?** - Y / N. Si la opción es Y, el sistema solicitará los datos de la zona existente.
- **Hosted Zone ID**: ID de la zona existente.
- **Host Name**: Nombre que se asignará a la zona.
- **Number of Imports**: Cantidad de registros a agregar.
- **Domain Name**.
- **IP**.
- **TTL**: Tiempo de vida del caché en segundos.
- **Type**: Consulta los tipos aceptados en esta liga: [Supported_DNS_Record_Types_Link](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html).

### Circle CI Config File Generator

Generación de archivo de Circle CI para el despliegue de aplicaciones.

- **Node version**.
- **Project type** - backend-api | frontend-spa.
- **Type of validation** - LinkCheck | Build | Both.
- **Project Environments**: Separa los entornos por comas (ejemplo: dev,prod).

### RDS Database

Servicio web que facilita la configuración, operación y escalado de una base de datos relacional en la Nube de AWS.

- **Database Name**: Nombre de la base de datos.
- **Database Instance**: Prefijo de la instancia para la base de datos.
- **Database Engine**: mariadb | mysql | oracle-ee | oracle-ee-cdb | oracle-se2 | oracle-se2-cdb | postgres | sqlserver-ee | sqlserver-se | sqlserver-ex | sqlserver-web.
- **User Name**: Nombre de usuario para iniciar sesión.
- **User Password**: Contraseña para inicio de sesión.
- **License**: license-included | bring-your-own-license | general-public-license (este parámetro solo aplica para las instancias de SQL Server).
