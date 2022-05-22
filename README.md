# <div align="center">
<table>
    <theader>
        <tr>
            <th><img src="https://github.com/rescobedoulasalle/git_github/blob/main/ulasalle.png?raw=true" alt="EPIS" style="width:50%; height:auto"/></th>
            <th>
                <span style="font-weight:bold;">UNIVERSIDAD LA SALLE</span><br />
                <span style="font-weight:bold;">FACULTAD DE INGENIERÍAS</span><br />
                <span style="font-weight:bold;">DEPARTAMENTO DE INGENIERÍA Y MATEMÁTICAS</span><br />
                <span style="font-weight:bold;">CARRERA PROFESIONAL DE INGENIERÍA DE SOFTWARE</span>
            </th>            
        </tr>
    </theader>
    
</table>
</div>

<div align="center">
<span style="font-weight:bold;">GUÍA DE LABORATORIO</span><br />
</div>

<table>
    <theader>
        <tr><th colspan="2">INFORMACIÓN BÁSICA</th></tr>
    </theader>
<tbody>

<tr><td>TÍTULO DE LA PRÁCTICA:</td><td>Docker</td></tr>
<tr><td colspan="2">RECURSOS:
    <ul>
    </ul>
</td>
</<tr>
<tr><td colspan="2">DOCENTES:
    <ul>
        <li>Richart Smith Escobedo Quispe  - r.escobedo@ulasalle.edu.pe</li>
    </ul>
</td>
</<tr>
</tdbody>
</table>

# Docker


[![Debian][Debian]][debian-site]
[![Git][Git]][git-site]
[![GitHub][GitHub]][github-site]
[![Vim][Vim]][vim-site]
[![Java][Java]][java-site]

#

## OBJETIVOS Y TEMAS

### OBJETIVOS
- Aprender a desplegar contenedores con Docker.

### TEMAS
- Docker.
- Docker vs VMs
- Arquitectura de Docker
- Comandos en Docker

## EJERCICIOS PROPUESTOS

-   1. Realice los cambios necesarios para que la imagen que ud creo a partir de un contenedor personalizado se pueda acceder al servidor web desde el equipo anfitríon.
    ```sh
    docker run -p 8088:80 rcd22image
    ```
-   2. Crear dos contenedores que puedan comunicarse: ping.

- Iniciamos las imagenes en la misma red.
- Corremos el servidor y el cliente.

![image](https://user-images.githubusercontent.com/79063417/168501033-19bb6798-cc8b-4dbe-934d-6536712e39ab.png)

![image](https://user-images.githubusercontent.com/79063417/168504561-efdb426d-56d7-4244-9172-1c95e7684de1.png)

- Usamos el comando start y attach para inicializar y dejar corriendo el server y el cliente

![image](https://user-images.githubusercontent.com/79063417/168508805-a9bc9afa-df7e-4c6d-befb-7676f40fb0a4.png)

-Configuración de red, maquina1: 
![image](https://user-images.githubusercontent.com/79063417/169671565-908eaa98-c3f7-4500-99bd-5279b8b4f313.png)

-Configuración de red, maquina2: 
![image](https://user-images.githubusercontent.com/79063417/169671571-6bff0ffb-16fe-48d5-8577-a9b6ca42ebf1.png)

-PING:
![image](https://user-images.githubusercontent.com/79063417/169671759-54e6a539-1ddf-4bab-bf2c-eaf07f3b2f46.png)

-   3. Investigar acerca de la ejecución de programas con interfaz gráfica dentro de contenedores Docker.

Proporcionar un contenedor Docker con acceso al socket X de su host es un procedimiento sencillo. La toma X se
encuentra en /tmp/.X11-unix en su anfitrión. El contenido de este directorio debe montarse en un volumen de Docker
asignado al contenedor. Necesitará utilizar el host modo de red para que esto funcione.
También debe proporcionar al contenedor un DISPLAY Variable ambiental. Esto le dice a los clientes X, sus programas de
gráficos, a qué servidor X conectarse. Ajustar DISPLAY en el contenedor por el valor de $DISPLAY en su anfitrión.
Puede envolver toda esta configuración en una docker-compose.yml depositar:

![image](https://user-images.githubusercontent.com/79063417/169719112-5b233601-fd6f-4f9c-833d-32e090f5b803.png)

Entonces necesitas crear un Dockerfile para su aplicación. A continuación, se muestra un ejemplo que ejecuta el
navegador web Firefox:

![image](https://user-images.githubusercontent.com/79063417/169719498-d82d9350-e70b-408c-85ab-ac0c028f6f51.png)

Ahora crea y ejecuta la imagen:

![image](https://user-images.githubusercontent.com/79063417/169719507-9e255523-1760-4838-87a9-79d2ae63d5cb.png)

Debería aparecer una nueva ventana de Firefox en su escritorio. La instancia de Firefox se ejecutará en el contenedor,
independientemente de cualquier otra ventana abierta de Firefox. El contenedor compartirá el socket X de su host, por lo
que Firefox en contenedor siempre aparecerá en su escritorio.
Este enfoque solo debe usarse cuando confía en su contenedor Docker. Exponer el servidor de visualización del host es un
riesgo de seguridad si no está completamente seguro de lo que hay dentro del contenedor.
CUESTIONARIO

#

## CUESTIONARIO

- ¿Qué son los "cgroups" del kernel de Linux? y ¿Qué diferencia más interesante encontró entre las versiones 1 y 2?

También llamados grupos de control, son una característica del kernel Linux que permite que los procesos se organicen en
grupos jerárquicos con el fin de limitar y monitorear el uso de varios tipos de recursos. Con cgroups cada proceso corre
en su propio espacio del kernel y de la memoria.
Algo que se resalta entre estas versiones es que a diferencia de v1, cgroup de la versión 2 tiene una única jerarquía de procesos y 
discrimina entre procesos, no entre subprocesos.

- ¿Qué son los "namespaces" del kernel de Linux? y ¿Cuáles son los tipos de "namespaces"?

Los namespaces de GNU/Linux permiten encapsular recursos globales del sistema de forma aislada, evitando que puedan
interferir con procesos que estén fuera del namespace, sin tener que recurrir a máquinas virtuales. Los tipos de
"namespaces" son los siguientes:
- mnt: controla el aislamiento de los distintos puntos de montaje.
- pid: encargado de asignar un nuevo PID a cada proceso.
- net: proporciona el aislamiento de los recursos asociados con el networking (devices, IPv4, IPv6, etc…)
- ipc: identificadores IPC de SysV
- uts: nombres de hosts y dominios
- user: identificadores de usuarios y grupos.


- ¿Qué diferencia puede resaltar entre LXC y libcontainer?

Que LXC se usó antes de Docker 0.9 como un controlador de ejecución por docker, y ofreció una interfaz de espacio de
usuario para las características de contención del kernel de Linux. Mientras que libcontainer es una abstracción, con el fin
de admitir una gama más amplia de tecnologías de aislamiento.

- Investigue acerca del malware Doki y explique brevemente.

Es un malware de Linux indetectable que explota técnicas indocumentadas para permanecer bajo el radar y apunta a
servidores Docker de acceso público alojados en plataformas de cloud populares, incluidas AWS, Azure y Alibaba Cloud.
Las caracteristicas de este malware son los siguientes:
* Ha sido diseñado para ejecutar comandos recibidos de sus operadores.
* Utiliza un explorador de bloques de criptomonedas Dogecoin para generar su dominio C2 en tiempo real
dinámicamente.
* Usa la biblioteca embedTLS para funciones criptográficas y comunicación de red,
* Crea URLs únicas con una vida útil corta y las usa para la descarga de payloads durante el ataque.

- ¿Hasta que punto la empresa RedHat se ha comprometido con el proyecto Docker?

La tecnología Docker utiliza el kernel de Linux y sus funciones, como los grupos de control y los espacios de nombre, para
dividir los procesos y ejecutarlos de manera independiente. El propósito de los contenedores es ejecutar varios procesos y
aplicaciones por separado para que se pueda aprovechar mejor la infraestructura y, al mismo tiempo, conservar la
seguridad que se obtendría con los sistemas individuales. Con Docker, podrá utilizar los contenedores como máquinas
virtuales muy livianas y modulares, y obtendrá la flexibilidad necesaria para crearlos, implementarlos, copiarlos y
trasladarlos de un entorno a otro, lo cual le permite optimizar sus aplicaciones para la nube.
Docker, por sí solo, puede gestionar contenedores individuales. Si comienza a utilizar cada vez más contenedores y
aplicaciones que se alojan en ellos con cientos de elementos, se dificultará su gestión y organización. En algún momento,
deberá cambiar el enfoque y agrupar los contenedores para prestar los servicios, como las redes, la seguridad y la
telemetría, entre otros, en todos los contenedores. Allí entra en juego Kubernetes. Docker no ofrece las mismas funciones
tipo UNIX que se obtienen con los contenedores tradicionales de Linux, como la capacidad para usar los procesos como
cron o syslog dentro del contenedor, junto con la aplicación. Esta tecnología también implica otras limitaciones, por
ejemplo, en cuanto a la eliminación de los procesos derivados de los secundarios después de borrar estos últimos, lo cual
se realiza de manera natural en los contenedores tradicionales de Linux. A pesar de que no resulte evidente a simple vista,
se pueden reducir estas complicaciones al modificar el archivo de configuración y establecer esas habilidades desde el
comienzo.

#

## REFERENCIAS
- https://www.tremplin-numerique.org/es/comment-executer-des-applications-gui-dans-un-conteneur-docker
- https://www.redhat.com/es/topics/containers/what-is-docker
- https://unaaldia.hispasec.com/2020/07/doki-el-nuevo-malware-de-linux-fija-como-objetivo-las-apis-de-contenedores-docker-mal-configurados.html
- https://www.desarrollo-web-br-bd.com/es/docker/diferencia-entre-lxc-y-libcontainer/1056301761/
- https://nebul4ck.wordpress.com/2016/08/12/namespace-linux/
-   [Sitio oficial del Proyecto Docker][Docker-site]
-   [Proyecto Moby][Moby-Github]
-   [Diapositivas "Contenedores de Linux y la nube del futuro" por Rami Rosen][Containers-PDF]
-   [Docker para un proyecto Joomla-MySQL][Joomla-MySQL]
-   [Tutorial de Docker en Youtube][Docker-Tutorial-Youtube]
-   [Cómo instalar y usar Docker en Ubuntu 20.04][Cómo instalar y usar Docker en Ubuntu 20.04]

#

[license]: https://img.shields.io/github/license/rescobedoulasalle/git_github?label=rescobedoulasalle
[license-file]: https://github.com/rescobedoulasalle/git_github/blob/main/LICENSE

[downloads]: https://img.shields.io/github/downloads/rescobedoulasalle/git_github/total?label=Downloads
[releases]: https://github.com/rescobedoulasalle/git_github/releases/

[last-commit]: https://img.shields.io/github/last-commit/rescobedoulasalle/git_github?label=Last%20Commit

[Debian]: https://img.shields.io/badge/Debian-D70A53?style=for-the-badge&logo=debian&logoColor=white
[debian-site]: https://www.debian.org/index.es.html

[Git]: https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white
[git-site]: https://git-scm.com/

[GitHub]: https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white
[github-site]: https://github.com/

[Vim]: https://img.shields.io/badge/VIM-%2311AB00.svg?style=for-the-badge&logo=vim&logoColor=white
[vim-site]: https://www.vim.org/

[Java]: https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=java&logoColor=white
[java-site]: https://docs.oracle.com/javase/tutorial/

[Docker-site]: https://www.docker.com/
[Moby-Github]: https://github.com/moby/moby
[Containers-PDF]: http://www.haifux.org/lectures/320/netLec8_final.pdf
[Joomla-MySQL]: https://dondocker.com/orquestando-contenedores-docker-para-tener-un-joomla-y-un-mysql-en-diferentes-hosts/
[Docker-Tutorial-Youtube]: https://www.youtube.com/watch?v=VeiUjkiqo9E#t=60

[Docker: A 'Shipping Container' for Linux Code]: https://web.archive.org/web/20130808043357/http://www.linux.com/news/enterprise/cloud-computing/731454-docker-a-shipping-container-for-linux-code/
[Tutorial de Docker: instalar y gestionar la plataforma de contenedores]: https://www.ionos.es/digitalguide/servidores/configuracion/tutorial-docker-instalacion-y-primeros-pasos/

[Docker-Hub]: https://hub.docker.com/

[Cómo instalar y usar Docker en Ubuntu 20.04]:https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-es


[![Debian][Debian]][debian-site]
[![Git][Git]][git-site]
[![GitHub][GitHub]][github-site]
[![Vim][Vim]][vim-site]
[![Java][Java]][java-site]

