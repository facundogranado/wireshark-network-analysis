#  Triage de Alerta – Anomalía en Tráfico TLS

##  1. Recepción de la alerta

Se recibe una alerta indicando:

**"Conexión TLS sospechosa hacia servidor externo con certificado inusual"**

- Tipo de alerta: TLS Anomaly
- Fuente: Monitoreo de red (laboratorio)
- Categoría: Encrypted Traffic Inspection

---

##  2. Validación inicial

Se inspecciona la captura de tráfico.

**Filtro aplicado en Wireshark:**
ip.addr == 192.168.1.25 and tls

Se valida:

- IP origen y destino
- Versión de TLS utilizada
- Server Name Indication (SNI)
- Certificado presentado por el servidor
- Cipher Suite negociado

---

##  3. Recolección de evidencia

### Hallazgos:

- Conexión TLS 1.2
- Certificado autofirmado
- Common Name no coincide con el dominio
- Validez extensa (10 años)
- Cipher suite poco común

No se observan errores de handshake.

Se exporta el handshake TLS para análisis del certificado.

---

##  4. Análisis técnico

### Hipótesis consideradas:

- Servidor legítimo mal configurado.
- Infraestructura interna de pruebas.
- Posible servidor C2 utilizando TLS para evadir inspección.

### Verificaciones realizadas:

- Revisión de campos del certificado:
  - Issuer
  - Subject
  - Validez
- Revisión del SNI.
- Análisis de frecuencia de conexiones.
- Correlación con eventos DNS previos (escenario simulado).

El uso de certificado autofirmado y parámetros inusuales aumenta el nivel de sospecha.

---

##  5. Clasificación

- Impacto potencial: Medio-Alto
- Probabilidad: Media
- Severidad asignada: Media-Alta

El uso de cifrado no implica benignidad. La anomalía en el certificado requiere seguimiento.

---

##  6. Decisión

### Acciones recomendadas:

- Verificar si el destino pertenece a infraestructura autorizada.
- Correlacionar con procesos activos en el endpoint.
- Revisar si existen conexiones periódicas.
- Implementar inspección TLS si la política lo permite.

**Estado:** Escalado a análisis extendido
