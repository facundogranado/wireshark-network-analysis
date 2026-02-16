# Triage de Alerta – Conectividad Externa Inusual

##  1. Recepción de la alerta

Se detecta:

**"Conexión saliente desde host interno hacia IP externa no habitual"**

- Tipo de alerta: Conectividad sospechosa
- Fuente: Monitoreo de red
- Categoría: Outbound Connection Monitoring

---

##  2. Validación inicial

Se inspecciona la captura de tráfico.

**Filtro aplicado en Wireshark:**
ip.addr == 192.168.1.25 and tcp


Se valida:

- IP destino
- Puerto destino
- Estado de la conexión (SYN, SYN-ACK, ESTABLISHED)
- Cantidad de intentos

---

##  3. Recolección de evidencia

### Observaciones:

- Múltiples intentos de conexión a puerto 443.
- Intervalos regulares (~10 segundos).
- Conexión establecida exitosamente.
- Transferencia mínima de datos.
- Duración corta de sesión.

Se registran timestamps y frecuencia de conexiones.

---

##  4. Análisis técnico

### Hipótesis consideradas:

- Aplicación legítima realizando check-in.
- Servicio en segundo plano.
- Posible beaconing hacia infraestructura remota.

### Verificaciones realizadas:

- Revisión de reputación de IP.
- Análisis de periodicidad.
- Correlación con actividad DNS previa.
- Evaluación de volumen de datos transferidos.

El patrón periódico con bajo volumen es consistente con comportamiento tipo beacon.

---

##  5. Clasificación

- Impacto potencial: Medio
- Probabilidad: Media
- Severidad: Media

No se observa exfiltración, pero el patrón amerita monitoreo.

---

##  6. Decisión

### Acciones recomendadas:

- Correlacionar con procesos activos en el host.
- Revisar logs del endpoint.
- Monitorear persistencia del patrón.
- Escalar si aumenta volumen o cambia comportamiento.

**Estado:** En observación activa

