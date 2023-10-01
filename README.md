# Lab2AdminRedes

# Configuración y verificación


Tabla de direccionamiento:

![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/625051e8-4c12-4723-b753-53f52e743936)


 
Subneteo
Paso 1: Selección del Rango de Direcciones IPv6:

Elegimos el rango de direcciones IPv6 2001:1200:A2::/64 como nuestro punto de partida. Este rango nos brinda suficiente espacio para asignar subredes a cada una de nuestras VLANs.

Paso 2: Determinación de la Cantidad de Subredes Requeridas:

Identificamos las VLANs que necesitamos y determinamos la cantidad de subredes necesarias, en nuestro caso, cinco subredes para Guest, Internal, ServerPrint, VOIP y Native.

Paso 3: Cálculo de la Máscara de Subred:

Para dividir el rango de direcciones en subredes más pequeñas, calculamos la máscara de subred adecuada. Dado que estamos utilizando /64 por defecto en IPv6, decidimos asignar /64 a cada una de nuestras subredes.

Paso 4: Asignación de Direcciones IPv6 a las Subredes:

Dividimos el rango 2001:1200:A2::/64 en cinco subredes con las siguientes direcciones base:

•	Guest: 2001:1200:A2:1::/64

•	Internal: 2001:1200:A2:2::/64

•	ServerPrint: 2001:1200:A2:3::/64

•	VOIP: 2001:1200:A2:4::/64

•	Native: 2001:1200:A2:5::/64

Cada una de estas subredes es lo suficientemente grande como para acomodar dispositivos y hosts dentro de su VLAN respectiva.


Para las otras redes la tabla queda de la siguiente manera: 

![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/0348f4ed-632a-4a0c-8f86-055639654b78)


 
Dhcpv6:
Para habilitar la configuración automática de redes IPv6 en nuestra topología, hemos empleado el servicio DHCPv6. En particular, en la red de Bogotá, disponemos de un servidor dedicado que opera este servicio con el propósito de asignar direcciones IPv6 de manera automática a todos los dispositivos que se conecten a la red. La configuración de este servidor no se limita únicamente a la asignación de direcciones IPv6; también nos permite ofrecer información crucial, como la puerta de enlace (Gateway) y los servidores DNS pertinentes.


A continuación, presentamos la estructura del servidor DHCP, que se encuentra diseñado de la siguiente manera:

![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/fa8b8214-39ee-425f-8e31-df97897fced2)

 

Y aquí un ejemplo de cómo se ve en un computador (PC2):

![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/61f7679c-b955-4d3d-9c31-82d4af3f6a36)

 
En el caso de la red de España no había un servidor DHCP por lo que esta configiracion se hace directamente desde el router, en este caso R2_ESP, aquí se utilizan unos comandos para asignarles las direcciones ipv6 a cada dispositivo de la red, algunos de los comandos son los siguientes: 

![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/18cca274-ff65-4098-ab87-adabe4aee6ec)


 

En este caso este seria para darle automáticamente la dirección ipv6 a al dispositivo que accede a la vlan 10, (Guest), pero se configura igual para cada vlan diferente.


En aras de garantizar que cada dispositivo tenga acceso a su VLAN correspondiente, se procedió a configurar minuciosamente cada uno de los switches involucrados en ambas redes. Es importante destacar que, en este escenario, la configuración aplicada a los switches de ambas redes fue idéntica.

Configuración de las VLANs:


La configuración de las VLANs se erige como una etapa fundamental en el proceso. Después de su creación, los puertos que enlazan con otros switches o con el router se establecen en modo "trunk". Esto permite que todos los dispositivos asociados a dichos puertos tengan acceso sin restricciones a todas las VLANs. Por otra parte, para los dispositivos que únicamente necesitan conectarse a una VLAN en particular, se configuran los puertos en modo "acceso". Esta configuración puntual desempeña un papel crítico al informar al servidor DHCPv6 sobre la pertenencia de cada dispositivo a su respectiva red.
Ventajas de esta Configuración:


Esta estrategia de configuración garantiza una gestión eficaz de las VLANs y optimiza el despliegue de recursos en la red. Al asignar puertos en modo "trunk" para interconexiones y puertos en modo "acceso" para dispositivos individuales, se logra un equilibrio entre la seguridad y la accesibilidad. Además, facilita el trabajo del servidor DHCPv6 al identificar claramente a qué red pertenece cada dispositivo, lo que resulta en una asignación de direcciones IPv6 más precisa y eficiente.


En resumen, la configuración de las VLANs desempeña un papel crítico en la organización y eficiencia de la red. La decisión de utilizar puertos en modo "trunk" o "acceso" se basa en las necesidades específicas de cada dispositivo y VLAN. Este enfoque no solo mejora la seguridad de la red al limitar el acceso solo a las VLANs pertinentes, sino que también optimiza el funcionamiento del servidor DHCPv6 al brindarle información precisa sobre la afiliación de los dispositivos a cada red. En última instancia, esta configuración contribuye a una red más eficiente y segura para todos los usuarios y dispositivos involucrados.


enrutamiento eigrp 1 y eigrpv6 


A continuación, se detalla la configuración realizada en los enlaces seriales entre los routers interconectados. Para esta configuración, se optó por asignar direcciones IPv4 pertenecientes a la red 190.90.2.0/24, las cuales se sometieron a un proceso de subneteo. Como resultado, se obtuvieron las siguientes redes disponibles:

•	190.90.2.1/30

•	190.90.2.5/30

•	190.90.2.10/30

•	190.90.2.6/30

•	190.90.2.21/30

•	190.90.2.2/30

•	190.90.2.9/30

•	190.90.2.19/30

•	190.90.2.18/30

•	190.90.2.22/30



Esta estrategia de asignación permitió que cada enlace serial compartiera el mismo espacio de red, lo que facilitó la comunicación efectiva entre ellos.



Por otro lado, en el caso de los enlaces seriales configurados con direcciones IPv6, se siguió la tabla de Subneteo correspondiente. Para el enrutamiento, se implementó el protocolo EIGRP, utilizando EIGRP 1 para la red de Internet y EIGRPv6 para los enlaces IPv6. Este enfoque garantizó una administración eficiente de la red y un óptimo funcionamiento de la comunicación en ambos entornos.
Para verificar que se realizó correctamente el enrutamiento EIGRP, en el caso de IPv4 utilizamos el comando #show ip eigrp neigh que por ejemplo en el router ISP_NET nos muestra lo siguiente:



![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/953840ad-0bdc-4728-99d8-c3364f1478d4)


 
Como podemos ver este tiene a tres “vecinos” ya que son sus 3 interfaces seriales que detectan a otros protocolos eigrp en el enlace correspondiente.



En el caso de ipv6 el comando es #show ipv6 eigrp neigh que por ejemplo en el router R1_BOG, nos muestra lo siguiente: 



![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/99787ad6-4d0f-4f4f-9d57-075ad920d778)

 


creación de túnel ipv6ip isatap:



La configuración del túnel ha sido un paso crucial en nuestra implementación, donde hemos empleado el protocolo IPv6IP ISATAP. Para comprender a fondo esta elección, es importante definir el protocolo ISATAP y su función en este contexto.



Protocolo ISATAP (Intra-Site Automatic Tunnel Addressing Protocol):



ISATAP es un protocolo que se utiliza para permitir la comunicación entre dispositivos IPv6 a través de redes IPv4. Su función principal es la de facilitar la transición de IPv4 a IPv6 en entornos donde coexisten ambas versiones de IP. ISATAP logra esto creando túneles virtuales que encapsulan paquetes IPv6 en paquetes IPv4 para su tránsito a través de una red IPv4.



Configuración del Túnel:



En nuestro caso, hemos configurado un túnel entre los routers ISP_BOG e ISP_ESP para permitir que los paquetes IPv6 atraviesen una red IPv4 de manera eficiente. El proceso de configuración implica varios pasos.



Paso 1: Asignación de ID al Túnel:



Para iniciar, asignamos un identificador (ID) al túnel, en este caso, hemos utilizado ID=0. El comando empleado para activar el túnel es "#interface tunnel 0."



Paso 2: Configuración de Parámetros del Túnel:



A continuación, configuramos los siguientes parámetros del túnel:


•	Tunnel Source: Especificamos la fuente del túnel, que se refiere a la interfaz o dirección IPv4 desde la cual se originará el túnel.



•	Dirección IPv6 del Túnel: Asignamos una dirección IPv6 al túnel para identificarlo y encapsular los paquetes IPv6.



•	Tunnel Destination: Definimos la dirección IPv4 de destino del túnel, que corresponde al otro extremo del túnel en el router ISP_ESP.



•	Protocolo: Indicamos el protocolo ISATAP como el utilizado para este túnel.



Ejemplo de Configuración para el Router ISP_BOG:



interface tunnel 0 tunnel source [Dirección IPv4 de origen] tunnel mode ipv6ip isatap tunnel destination [Dirección IPv4 de destino] ipv6 address [Dirección IPv6 del túnel] 


Para el router ISP_BOG, la configuración del túnel quedaría de la siguiente manera:



![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/8f568958-4d27-41bc-bf0d-99f4c3c623c1)

 

Como se puede observar también se configura el protocolo EIGRP en este túnel.



Esta configuración permite que los paquetes IPv6 sean encapsulados en paquetes IPv4 y viajen a través del túnel desde ISP_BOG a ISP_ESP, facilitando así la comunicación IPv6 en nuestra red.



El uso de ISATAP en esta implementación es esencial para habilitar la coexistencia de IPv4 e IPv6 y garantizar la conectividad sin problemas de los dispositivos en nuestra red.





enrutamiento para direcciones ipv6:


En el contexto de nuestro proyecto, se ha vuelto esencial implementar el enrutamiento IPv6, ya que es necesario direccionar de manera efectiva los paquetes hacia destinos específicos. En particular, en este laboratorio, se nos ha requerido redirigir los paquetes generados tanto en la red de Madrid como en la red de Bogotá hacia nuestros servidores. Este redireccionamiento se hace necesario debido a que los dispositivos en ambas redes requieren acceder a un sitio web alojado en los servidores. Para lograr este enrutamiento IPv6, utilizamos el comando "ipv6 route".


El Comando "ipv6 route" y su Funcionalidad:


El comando "ipv6 route" desempeña un papel fundamental en la configuración y gestión de rutas IPv6 en nuestros routers. Su función principal es especificar cómo los paquetes IPv6 deben ser enrutados dentro de la red. Este comando permite al administrador definir rutas específicas para los paquetes, indicando el camino que deben seguir para llegar a su destino final. Cada entrada creada con "ipv6 route" consta de dos partes clave:


1.	Dirección de destino IPv6: Esta dirección especifica la red o el host al que se desea llegar.
   
   
2.	Próximo salto (Next Hop): Esta es la dirección IPv6 del siguiente nodo en la ruta que se utilizará para reenviar los paquetes hacia su destino.

   
Ejemplo de Configuración con "ipv6 route":


Para nuestro escenario, configuramos las rutas de la siguiente manera:


ipv6 route [Dirección de Destino] [Próximo Salto]

Esto asegura que los paquetes generados en las redes de Madrid y Bogotá sean dirigidos correctamente hacia los servidores. Los dispositivos en ambas redes pueden acceder al sitio web alojado en los servidores, ya que el enrutamiento IPv6 les proporciona la guía necesaria para alcanzar su destino.



Verificación de las Rutas con "#show ipv6 routes":


Para verificar la correcta configuración de las rutas IPv6 en nuestros routers, utilizamos el comando "#show ipv6 routes". Este comando nos muestra una lista detallada de las rutas configuradas en el router y proporciona información crucial sobre las rutas, como la dirección de destino, la métrica y el próximo salto. Un ejemplo de cómo se visualiza esto en el router ISP_BOG se muestra a continuación:


![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/0401e7b6-46c8-48ca-bf9e-6941b024b7c3)

 

Este comando es fundamental para asegurarse de que las rutas estén configuradas correctamente y de que el enrutamiento IPv6 funcione sin problemas en nuestra red. De esta manera, garantizamos que los dispositivos en las redes de Madrid y Bogotá puedan acceder sin dificultades al recurso web hospedado en nuestros servidores.






acces list ipv6:



En la etapa actual de nuestro proyecto, hemos asegurado la disponibilidad de la página web alojada en nuestros servidores y hemos verificado que todos los dispositivos pueden acceder a ella sin dificultades utilizando el nombre de dominio "cadasa.net".


 
![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/655f5feb-0523-494c-88e2-f24c725a5f38)



Ahora en el informe que requieren que ciertos dispositivos accedan a los servidores a través del puerto 80, mientras que otros deben hacerlo a través del puerto 443. En el caso de la red de Bogotá, específicamente, se ha determinado que los dispositivos PC1 y PC3 deben acceder a través del puerto 80, mientras que los demás deben utilizar el puerto 443.
Uso de Access List IPv6 (Lista de Control de Acceso IPv6):




Para implementar esta restricción y permitir el acceso diferenciado a los puertos, hemos empleado una herramienta clave llamada "Access List IPv6" o "Lista de Control de Acceso IPv6". Una Access List IPv6 es una lista de reglas que se utiliza para controlar el flujo de paquetes en una red IPv6. Cada regla define condiciones específicas que los paquetes deben cumplir para ser permitidos o denegados.
Configuración de Access List IPv6:


El proceso para lograr esta configuración implica varios pasos:


Paso 1: Creación de la Access List IPv6:


Primero, creamos una Access List IPv6 utilizando el comando "#ipv6 access-list [nombre]". En nuestro caso, hemos nombrado la Access List como "HTTP-HTTPS."


Paso 2: Definición de las Reglas de Acceso:


A continuación, definimos las reglas dentro de la Access List para restringir el acceso a ciertas redes a través de determinados puertos. Para el caso de PC1 y PC3 en la red de Bogotá, la configuración se vería de la siguiente manera:


#ipv6 access-list HTTP-HTTPS 


#deny tcp [Dirección de Red] any eq 443 


#permit tcp [Dirección de Red] any eq 80 



![image](https://github.com/CamiloSanchezCuestas/Lab2AdminRedes/assets/110070037/70d3659d-8ed7-4d40-8ba4-042ce5d09912)


 
Esto significa que las redes con la dirección 2001:1200:A2:1::/64 no podrán acceder al puerto 443, pero se les permitirá el acceso al puerto 80.


Esta configuración permite una diferenciación clara en el acceso a los servidores, asegurando que los dispositivos PC1 y PC3 en la red de Bogotá puedan utilizar el puerto 80, mientras que otros dispositivos accedan a través del puerto 443. Las Access Lists IPv6 son una herramienta esencial para administrar y controlar el flujo de tráfico en una red IPv6, lo que garantiza una mayor seguridad y eficiencia en la distribución de recursos y servicios.


