# Proyecto: P1

# B1. La red

## Creación de la VPC

Se ha creado una VPC llamada **libreria-vpc** con el bloque CIDR:

- 10.0.0.0/16


---

## Creación de la subred pública

Se ha creado una subred pública llamada **libreria-publica** con el bloque CIDR:

- 10.0.1.0/24


### Subred privada

### Asociación de red

---

## Creación del Internet Gateway

Se ha creado un Internet Gateway y se ha asociado a la VPC para permitir el acceso a Internet.


---

## Tabla de rutas

Se ha creado una tabla de rutas pública con las siguientes entradas:

| Destino | Objetivo |
|----------|----------|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | Internet Gateway |

### ¿Por qué la subred es pública?

La subred es pública porque está asociada a una tabla de rutas que contiene una ruta por defecto (0.0.0.0/0) dirigida a un Internet Gateway. Esto permite que las instancias dentro de la subred puedan acceder a Internet y recibir tráfico externo.

---

# B2. Seguridad

## Grupo de seguridad

Se ha creado el grupo de seguridad **libreria-web-sg**.

### Reglas de entrada configuradas

- HTTP (80) desde cualquier dirección IPv4.
- SSH (22) únicamente desde mi dirección IP pública.


### ¿Por qué SSH solo se abre a mi IP?

El acceso SSH se restringe a mi dirección IP pública para evitar accesos no autorizados y mejorar la seguridad de la infraestructura.

---

# B3. Servidor web

## Creación de la instancia EC2

Se ha desplegado una instancia Amazon EC2 con la siguiente configuración:

- Nombre: libreria-web
- Sistema operativo: Amazon Linux 2023
- Tipo de instancia: t3.micro
- VPC: libreria-vpc
- Subred: libreria-publica
- Grupo de seguridad: libreria-web-sg



---

## Conexión SSH

Se ha establecido conexión SSH correctamente con la instancia EC2 para realizar tareas de administración.


---

## Servidor web

Se ha instalado y configurado un servidor web accesible mediante la dirección IP pública de la instancia.

La página web muestra información personalizada sobre la librería, incluyendo horario, dirección y una recomendación de lectura.

### Librería creada en una segunda EC2 por error

### EC2 final con el script de usuario

URL:

http://3.80.169.23/


---

## Comprobación

Se verificó el correcto funcionamiento del servidor web accediendo desde un navegador a la dirección IP pública de la instancia.

---

# B4. Cálculo de costes

Se ha utilizado AWS Pricing Calculator para estimar el coste de mantener el servidor web encendido las 24 horas del día durante todo el mes en la región us-east-1 (N. Virginia).

**Coste mensual estimado:** 3,80 USD/mes.

**Coste anual estimado:** 45,60 USD/año.

**Enlace de la estimación:**

https://calculator.aws/#/estimate?id=59847f74d1bbb98de8b7f1908e7ca9969408fd2c

### Posible reducción de costes

El coste podría reducirse deteniendo la instancia cuando no se utilice o utilizando instancias con menos recursos si la carga de trabajo fuese menor.


---

# Diagrama de arquitectura

La infraestructura desplegada está formada por:

- Una VPC personalizada.
- Una subred pública.
- Un Internet Gateway.
- Una tabla de rutas pública.
- Un grupo de seguridad.
- Una instancia EC2 con servidor web.

El tráfico accede desde Internet a través del Internet Gateway, pasa por la subred pública y llega a la instancia EC2 protegida por el grupo de seguridad.

### Diagrama

---

# Uso de IA

Para la realización de este proyecto se ha utilizado Microsoft Copilot como herramienta de apoyo.

## Prompt utilizado

> Indícame cómo y dónde debo añadir el script en una EC2 nueva en AWS, teniendo en cuenta el error cometido anteriormente.

## Error detectado

Durante el desarrollo del proyecto me equivoqué al crear la infraestructura. Inicialmente lancé una instancia EC2 sin configurar correctamente los datos de usuario y además creé recursos adicionales que no eran necesarios para completar el nivel básico del proyecto.

## Corrección realizada

Se revisó el enunciado oficial del proyecto y se desplegó una nueva instancia EC2 configurando correctamente los datos de usuario para automatizar la instalación y configuración del servidor web.

---

# Conclusiones

Durante este proyecto se ha desplegado una infraestructura básica en AWS utilizando servicios de red, seguridad y computación.

Se ha configurado una VPC personalizada, una instancia EC2 accesible desde Internet y un servidor web funcional. Además, se ha realizado una estimación económica mediante AWS Pricing Calculator y se ha documentado todo el proceso seguido.

El proyecto ha permitido comprender el funcionamiento básico de una infraestructura en la nube, incluyendo redes, seguridad, despliegue de servidores web y estimación de costes.


