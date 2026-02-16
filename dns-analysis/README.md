#  Triage de Alerta – Actividad DNS Anómala

##  1. Recepción de la alerta

Se recibe una alerta indicando:

**"Volumen inusual de consultas DNS desde el host 192.168.1.25"**

- Tipo de alerta: Comportamiento anómalo
- Fuente: Monitoreo de red
- Categoría: Network Anomaly Detection

---

##  2. Validación inicial

Se procede a validar la alerta en captura de tráfico.

**Filtro aplicado en Wireshark:**
ip.addr == 192.168.1.25 and dns

Se valida:

- Timestamp del evento
- IP origen
- Dominio consultado
- Cantidad de consultas
- Tipo de registro DNS solicitado

---

##  3. Recolección de evidencia

### Hallazgos:

- Más de 50 consultas en menos de 2 minutos.
- Dominio repetido en múltiples requests.
- Intervalos regulares (~5 segundos).
- Respuestas válidas (sin NXDOMAIN).
- Consultas tipo A.

---

##  4. Análisis técnico

### Hipótesis consideradas:

- Aplicación legítima realizando polling.
- Script automatizado.
- Posible comportamiento de beaconing (C2).

### Verificaciones realizadas:

- Revisión de patrón temporal (intervalos constantes).
- Análisis de periodicidad.
- Revisión de reputación del dominio.
- Correlación con procesos activos en el host.

---

##  5. Clasificación

- Impacto potencial: Medio
- Probabilidad: Media
- Severidad asignada: Media

No se detecta exfiltración directa, pero el patrón es consistente con comportamiento automatizado tipo beacon.

---

##  6. Decisión

### Acciones recomendadas:

- Correlacionar con procesos activos en el endpoint.
- Validar si existe software legítimo generando consultas.
- Mantener monitoreo continuo.
- Escalar si se detecta tráfico adicional sospechoso (HTTP/HTTPS, DNS TXT, etc).

**Estado:** En observación

