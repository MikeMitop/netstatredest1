# Análisis  con `netstat` (30 minutos)

Este archivo explica **cómo se realiza el proceso de capturar** la actividad de red con `netstat`, **qué significa** lo que aparece en la traza y **cómo analizarla** 

---

##  Objetivo:
- Registrar por ~30 minutos las conexiones del host.
- Entender estados de TCP (**ESTABLISHED**, **TIME_WAIT**, **CLOSE_WAIT**), puertos típicos (80/443/53/67–68) y **sockets UNIX**
- Conectarlo con **Aplicación, Transporte, Red, Enlace/Física** del modelo OSI.

---

##  Requisitos
- Linux.
- Paquete `net-tools` (para `netstat`):
  ```bash
  sudo dnf install -y net-tools```

### Capturar una muestra cada 10 s, guardando al archivo


```netstat -c 10 > traza.txt```


### Dejarlo ~30 min y detener con Ctrl + C

---------------------------------------------------------------------------------------



# ¿Qué significa cada columna del archivo?:

***Proto:*** Protocolo de transporte (TCP o UDP). 

***Recv-Q / Send-Q:*** Bytes en cola pendientes de recibir/enviar.

***Local Address: IP:*** Puerto del  equipo local.

***Foreign Address:*** IP:puerto del destino (servidor).

***State (TCP):*** Estado de la conexión.

***UNIX*** Comunicación local entre procesos


---------------------------------------------------------------------------------------


### Significado de estados TCP

***STABLISHED*** → Conexión activa intercambiando datos en el momento.

***TIME_WAIT*** → La conexión terminó

***CLOSE_WAIT*** → El remoto cerró primero; la aplicación aún no cerró el socket.

***LISTEN*** → El puerto está esperando conexiones entrantes.

*UDP es “sin conexión”, por eso no muestra estados.*

---------------------------------------------------------------------------------------



## Puertos y servicios comunes:

**443 (HTTPS):** Tráfico web cifrado 

**80 (HTTP):** Web sin cifrar 

**53 (DNS):** Resolver nombres de dominio.

**67/68 (DHCP, UDP):** renovación de dirección IP.

----------------------------------------------------------------------------------------

# Relación con el modelo OSI:

**Aplicación:** El programa que genera tráfico (En este caso, YouTUbe)

**Transporte (TCP/UDP):**

TCP mantiene estados (tales como ESTABLISHED, TIME_WAIT…).

**Red (IP):** Direcciones IPv4/IPv6 que aparecen en Local/Foreign Address.

**Enlace/Física:** aquí viven ideas de capacidad del medio (Cantidad de bits por segundo que pasan) y el delay (tiempo de viaje)

