# InvestigacionRedes

### Actividad: Fundamentos de Redes ### 

## **CONCEPTOS**

Router El router es el dispositivo de entrada a internet desde nuestro ordenador. Su función es interconectar redes y determinar la mejor ruta para los paquetes enviados. Ppera en la Capa 3 (Red) del modelo OSI. Sería como la oficina del servicio postal, Tu envías una carta internacional, el cartero la lleva a la oficina (router) y ahí decicen la mejor ruta para hacerla llgar al otro lado del mundo.

Switch: El switch recueda las direcciones MAC de los dispositivos que tiene conectados, lo que permite que envié datos únicamente al destinatario correcto. Opera en la Capa 2 (Enlace de Datos) del modelo OSI. El switch, sería como pararse en la oficina e ir a darle directamente el mensaje a mi colega, siendo que pude haberlo vociferado, pero todos habrían escuchado.

Hub: El HUB es una especie de "espacio común" donde toda la información que pasa por el, se disponibiliza a todos los conectados. Su función es recibir información y enviarla a todos los dispositivos conectados este, independientemente de si era direccionado a ellos. Opera en la Capa 1 (Capa Física) del modelo OSI. El HUB seria çomo un mailing, que envío a todos los colegas de la ofinina.

**¿Qué hace el router con los paquetes de datos?**

El router realiza 4 procesos fundamentales:
① Recibe el paquete y lee la IP destino
② Consulta su Tabla de Enrutamiento
③ Aplica NAT (Network Address Translation)
④ Reenvía el paquete por la interfaz correcta

**¿Cómo decide un switch a dónde enviar la información?**

El switch usa un proceso de aprendizaje automático basado en direcciones MAC. Son 3 etapas:
Etapa 1 — Aprendizaje
Etapa 2 — Decisión de envío (Forwarding)
Etapa 3 — Si no conoce el destino (Flooding)

**¿Por qué el hub es considerado obsoleto?**

Razón 1 — Colisiones constantes (El problema más grave)
Razón 2 — Seguridad nula
Razón 3 — Desperdicio de ancho de banda

**¿Qué rol cumple el router cuando tú haces una petición a una API?**
(Ej: `fetch("https://api.miapp.com")`)

El router hace 3 cosas esenciales:
① Traduce tu IP privada a pública (NAT)
Tu PC tiene IP 192.168.1.10 pero Internet no la entiende. El router la convierte a tu IP pública real.

② Elige el mejor camino hacia el servidor
Consulta su tabla interna y decide por dónde mandar el paquete, pasando por varios routers hasta llegar al destino.

③ Devuelve la respuesta a TU PC
Cuando el servidor responde, el router sabe exactamente a cuál dispositivo de tu casa entregarle la respuesta.

**¿Por qué un switch es importante en un backend o data center?**

En un datacenter hay **muchos servidores comunicándose al mismo tiempo.** El switch garantiza que esa comunicación sea rápida y directa.

**Clave:** En microservicios, cuando tu API llama a otros 4 servicios internos, el switch es quien los conecta directamente y a máxima velocidad.

**¿Qué problemas de red podrían afectar tu aplicación aunque tu código esté “correcto”?**

- Latencia alta, Red congestionada o servidor lejano.
- Timeour sin controlar, la app espera para siempre.
- DNS caído, El dominio no se puede resolver.
- CORS, El navegador bloquea la respuesta por seguridad.

**Escenario:**

> “Tu aplicación está en producción, pero los usuarios no pueden acceder.”

**¿Podría ser problema de router? ¿por qué?**
Sí, y es lo más probable. El router es la puerta de entrada a tu servidor.

**¿Podría ser problema de switch? ¿por qué?**
Sí, aunque es menos frecuente. Si el switch falla, los servidores quedan incomunicados entre sí.

**¿Cómo distinguir si es problema de red o de código?**
El siguiente diagrama nos ayuda a diagnosticarlo:

¿La app no responde?
        │
        ▼
¿Puedes hacer ping al servidor?
    │               │
   NO               SÍ
    │               │
Problema          ¿El puerto responde?
de RED 🔴         (telnet ip 443)
                  │           │
                 NO           SÍ
                  │           │
               Firewall/    Problema
               Router 🔴    de CÓDIGO 🟡

**Crear una analogía:**

**Router** = Cuando llega un visitante (paquete), el portero revisa a qué edificio va (IP destino), consulta su mapa (tabla de enrutamiento) y lo manda por la calle correcta hacia su destino, aunque esté en otro país.

**Switch** = Conoce a cada empleado por su cara (dirección MAC) y sabe exactamente en qué escritorio está. Cuando llega un mensaje para María, se lo entrega solo a María, nadie más se entera.

*Hub** = Cada vez que alguien habla, grita el mensaje a toda la oficina sin importar para quién era. Todos escuchan todo, no hay privacidad, y si dos personas hablan al mismo tiempo se arma un caos.

## Presentación
Cada uno debe explicar:

1. Diferencia clave entre router, switch y hub
2. Un ejemplo real en desarrollo
3. Su analogía

## BONUS

**¿Dónde entra un **load balancer** en todo esto?**

Un Load Balancer es como un Switch inteligente de nivel superior — pero en vez de distribuir paquetes, distribuye usuarios entre varios servidores. El router lleva el tráfico hasta tu puerta, el load balancer decide cuál servidor lo atiende.

INTERNET
    │
 [ROUTER]
    │
[LOAD BALANCER] 
    │
┌───┼───┐
S1  S2  S3 


**¿Qué relación tiene esto con cloud (AWS, Azure, etc.)?**

La nube no elimina estos conceptos — los virtualiza. Todo sigue existiendo, pero ya no lo ves físicamente.
