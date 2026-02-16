#  Triage de Alerta – Tráfico HTTP No Cifrado


##  1. Recepción de la alerta

Se detecta tráfico HTTP (no cifrado) hacia un servidor externo desde un equipo interno.

- Tipo de alerta: Comunicación no cifrada
- Fuente: Monitoreo de red (laboratorio)
- Categoría: Insecure Protocol Usage

---

##  2. Validación inicial

Se inspecciona la captura de red.

**Filtro aplicado:**
ip.addr == 192.168.1.25 and http


Se confirma:

- Tráfico HTTP sin TLS.
- Comunicación saliente hacia IP externa.
- Método HTTP utilizado.

---

##  3. Recolección de evidencia

### Observaciones:

- Método GET.
- Headers visibles.
- Respuesta 200 OK.
- Contenido transmitido en texto plano.
- Sin envío de credenciales observadas.

Se revisa el payload para identificar posible fuga de información.

---

##  4. Análisis técnico

Se analiza:

- Tipo de recurso descargado.
- Presencia de parámetros sensibles en URL.
- Frecuencia de conexiones.
- Persistencia del destino externo.

Se determina que el tráfico corresponde a navegación básica sin envío de datos sensibles.

---

##  5. Clasificación

- Impacto: Bajo
- Probabilidad de riesgo: Baja
- Severidad: Baja

Se clasifica como uso de protocolo inseguro sin evidencia de explotación.

---

##  6. Decisión

### Acciones recomendadas:

- Recomendar migración a HTTPS.
- Verificar políticas internas de uso de protocolos.
- No requiere escalamiento.

**Estado:** Cerrado – Informativo

