# Informe Final  
**Título del Proyecto:** Proyecto de monitoreo de sensores IoT mediante Zabbix para gestión de redes  

**Autores:**  
- Cristian Ancízar Rojas Herrera  
- Carlos Andrés Velásquez Saavedra  

**Profesor:**  
Ing. Jaider Ospina Navas  

**Universidad Militar Nueva Granada - UMNG**  
Facultad de Ingeniería  
Tecnología en Telecomunicaciones  
19 de noviembre de 2025  

---

## Tabla de Contenido
- Resumen (Abstract)
- Palabras Clave
- Introducción
- Objetivos
- Marco Teórico
- Metodología
- Resultados o Discusión
- Conclusiones
- Referencias
- Anexos  

---

## Resumen
Este proyecto se centró en la concepción e implementación parcial de un sistema de monitorización remota para variables ambientales (temperatura y humedad), utilizando una arquitectura basada en **Arduino UNO con Shield Ethernet** como nodo de adquisición de datos y la plataforma **Zabbix** instalada en una máquina virtual (**VMware**) como sistema de gestión y visualización central.  

El objetivo fundamental era establecer una solución que permitiera la visualización en tiempo real de los datos de los sensores y la configuración automática de alertas ante desviaciones.  

A pesar de haber logrado la conectividad de red, la integración funcional del monitoreo de datos no pudo completarse debido a:  
- Limitación en la documentación de referencia.  
- Falla persistente en la comunicación del Agente Zabbix entre Arduino y el servidor.  

**Conclusión:** Se documenta el proceso, logros de conectividad y limitaciones técnicas. Se recomienda explorar firmware específico o protocolos alternativos (trappers, MQTT) para completar la telemetría ambiental.  

---

## Palabras Clave
Monitoreo remoto, Variables ambientales, Temperatura, Humedad, Arduino UNO, Shield Ethernet, Zabbix, VMware, Adquisición de datos, Gestión de red, Conectividad de red, Servidor Zabbix, Agente Zabbix, Fallo de conexión, Implementación parcial, Documentación, Limitaciones  

---

## Introducción
La necesidad de una administración de infraestructura proactiva y la creciente penetración del IoT justifican el uso de plataformas de monitorización de alto rendimiento.  
Zabbix se destaca como solución **open-source** robusta y adaptable.  

El proyecto buscó:  
- Integrar hardware (Arduino UNO + Shield Ethernet) con Zabbix en VM.  
- Configurar hosts, ítems y triggers.  
- Resolver fallas de conectividad inter-sistema.  

**Limitación:** No se logró la visualización de datos en Zabbix por incompatibilidad de integración.  

---

## Objetivos

### Objetivo General
Diseñar, configurar y validar un **Sistema de Monitoreo Integral (SMI)** para indicadores ambientales clave (temperatura y humedad), interconectando Arduino con Zabbix.  

### Objetivos Tácticos
1. **Infraestructura de Backend y Virtualización**  
   - Instalar VMware y desplegar Servidor Zabbix.  
   - Configurar backend de base de datos.  

2. **Interoperabilidad de Red**  
   - Configurar subredes, gateways e IPs.  
   - Asegurar conectividad bidireccional (ping).  
   - Configurar firewall para puerto 10051.  

3. **Subsistema de Adquisición de Datos**  
   - Programar firmware para lectura de sensores (DHT11/22).  
   - Implementar protocolo de reporte (Agente Zabbix o trappers).  

4. **Evaluación de Integración**  
   - Diagnóstico de fallas (timeout, parsing, rechazo de conexión).  
   - Documentar lessons learned.  

---

## Marco Teórico

### 1. Plataforma de Adquisición de Datos
- **Arduino UNO (ATmega328P)**: lectura de sensores de temperatura y humedad.  
- **Shield Ethernet (W5100/W5500)**: conectividad TCP/IP.  

### 2. Sistema de Gestión de Redes Empresarial
- **Zabbix**: NMS distribuido para centralización de datos.  
- Métodos de recolección: Agentes, SNMP, Trappers.  
- Estrategia: Agente Activo (Arduino → Zabbix Sender).  

### 3. Entorno de Operación
- **VMware**: aislamiento y simulación de servidor.  
- **Conectividad crítica**: tráfico del Agente debe llegar al puerto 10051/TCP del servidor.  

---

## Metodología

### Fase I: Preparación del Entorno
- Instalación de Zabbix Server en VM Linux.  
- Configuración de base de datos (PostgreSQL/MySQL).  
- Ensamblaje de Arduino + Shield + sensor DHT11.  
- Carga de firmware Arduino-Zabbix-Agent.  

### Fase II: Conectividad de Red
- Configuración de VM en modo **Bridge**.  
- Pruebas ICMP (ping) bidireccional.  
- Configuración de firewall para puerto 10051.  

### Fase III: Configuración de Monitoreo
- Definición de Host en Zabbix.  
- Creación de ítems (temperature, humidity).  
- Diagnóstico: Host permaneció en estado *Unknown*.  

---

## Resultados y Discusión

### Logros
- Infraestructura de red operativa.  
- Conectividad IP confirmada.  
- Servidor Zabbix desplegado correctamente.  
- Hardware ensamblado y firmware cargado.  

### Fallo Crítico
- Host en estado *Unknown*.  
- Paquetes enviados no compatibles con protocolo Zabbix.  
- Posible incompatibilidad de claves de ítems.  

### Implicaciones
- Documentación incompleta dificultó troubleshooting.  
- No se alcanzó la fase de dashboards ni triggers.  

---

## Conclusiones

1. **Éxitos**  
   - Virtualización y despliegue de Zabbix.  
   - Conectividad IP estable.  
   - Definición lógica de host e ítems.  

2. **Fallo Crítico**  
   - Incompatibilidad del protocolo Zabbix Agent en Arduino.  
   - Documentación insuficiente para debugging.  

3. **Lecciones Aprendidas**  
   - Agentes no oficiales generan sobrecarga de debugging.  
   - Protocolos alternativos (MQTT, Trappers) son más viables.  
   - Se establecieron bases para futuras iteraciones.  

---

## Recomendaciones

1. **Migración de Protocolo**  
   - Usar **Zabbix Trappers/Sender**.  
   - Integrar **MQTT** con broker (ej. Mosquitto).  
   - Implementar **HTTP/HTTPS Webhooks** como puente.  

2. **Validación y Debugging**  
   - Verificar compatibilidad de versiones.  
   - Usar Wireshark para inspección de payload.  

3. **Documentación**  
   - Establecer correspondencia entre claves en firmware y Zabbix.  
   - Buscar soluciones en foros especializados.  
![           ](1.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](2.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](3.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](4.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](5.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](6.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](7.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](8.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](9.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](10.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](11.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](12.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](13.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](14.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](15.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](16.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](17.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](18.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](19.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](20.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](2.jpg1)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](22.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](23.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](24.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](25.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](26.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](27.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](28.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](29.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](30.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](31.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](32.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](33.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](34.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](35.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](36.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](37.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](38.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](39.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](40.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](41.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](42.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](43.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](44.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](45.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](46.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](47.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](48.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](49.jpg)
![C:\Users\Pc\Documents\QUINTO SEMESTRE\GESTION DE RED\Imagen Proyecto](EsquemaProyectoFinal.jpg)
---
