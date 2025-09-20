# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 5 - Evaluación de Seguridad con STRIDE_

## 👥 Integrantes del equipo
- Valentina Rodríguez Romero  
- Wilson Santiago Bonilla Guevara  
- Juan Andrés Lacouture Daza  

## 🧠 Descripción general del trabajo
El objetivo del taller fue aplicar el marco **STRIDE** a un componente crítico del sistema del cliente **Compulens & Llanes SAS**, con el fin de identificar amenazas, evaluar impactos y proponer controles de mitigación.  
El trabajo se desarrolló en dos fases: primero la práctica en clase con el caso base **EdukIT** (plataforma educativa), y posteriormente la aplicación al cliente real, tomando como foco el **Backend de Pedidos**.

## 🔧 Proceso de desarrollo
- En clase se revisó el marco STRIDE y se ejercitó con EdukIT, evaluando amenazas en accesos, contenidos y pagos.  
- Para el cliente real, se seleccionó el **Backend de Pedidos** porque concentra la lógica principal: integra clientes, operadores, ERP y pagos, además de manejar datos sensibles (pedidos, datos ópticos y facturación).  
- Se elaboró una tabla en Excel con amenazas por categoría STRIDE, vectores de ataque, impacto esperado en términos de confidencialidad, integridad y disponibilidad, y controles propuestos.  
- Se generaron dos visiones: **riesgo inicial** y **riesgo residual** tras aplicar las recomendaciones, incluyendo una **matriz de calor (Probabilidad × Impacto)** para visualizar la priorización.  
- Finalmente se investigaron buenas prácticas de seguridad en el sector salud/óptica aplicables al caso.

## 🧩 Análisis del modelo propuesto
- **Estructura**: El análisis STRIDE cubrió seis dimensiones de seguridad en el Backend de Pedidos (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service y Elevation of Privilege).  
- **Necesidades del cliente**: Las amenazas mapeadas responden directamente a riesgos actuales: doble digitación, exposición de datos sensibles y ausencia de trazabilidad robusta.  
- **Supuestos**: Se asumió un despliegue híbrido (ERP on-premise + app en nube), sesiones con autenticación básica a reforzar, y ausencia inicial de observabilidad.  

## 📈 Tabla STRIDE del cliente
> (Se adjunta el archivo `tabla-stride-cliente.xlsx` con el detalle de amenazas, impacto esperado, controles propuestos, nivel de riesgo inicial y residual, más la matriz de calor).

## 📋 Actores, entidades o componentes evaluados

| Componente evaluado | Razón de selección | Riesgo principal | Controles propuestos |
|---------------------|-------------------|-----------------|----------------------|
| Backend de Pedidos  | Núcleo del sistema, conecta clientes, ERP y pagos | Exposición de datos y manipulación de pedidos | MFA, RBAC, cifrado, logging inmutable, autoescalado, WAF, validaciones server-side |

## 🔍 Investigación complementaria
### Tema investigado:
Buenas prácticas de seguridad en el sector salud/óptica para sistemas híbridos de pedidos y facturación.

### Resumen:
En este sector, la **protección de datos personales y clínicos** es prioritaria:  
- Se recomiendan **controles de acceso estrictos** con autenticación multifactor (MFA) y autorización basada en roles (RBAC/ABAC).  
- **Cifrado en tránsito y en reposo** es obligatorio para datos sensibles (pedidos, medidas ópticas, facturación).  
- La **observabilidad** (métricas, logs y trazas centralizadas) es clave para detectar incidentes y reducir tiempos de respuesta (MTTR).  
- Las integraciones con sistemas externos (ERP y pagos) deben usar **mTLS, firmas HMAC y validación de callbacks** para prevenir suplantaciones y alteraciones de datos.  
- Para disponibilidad, implementar **autoescalado y pruebas de carga**, junto con respaldos periódicos y planes de recuperación.  

Estas medidas, aplicadas al Backend de Pedidos, reducen significativamente los riesgos identificados en el análisis STRIDE y fortalecen la resiliencia del sistema.

---

_Este documento hace parte de la entrega del Taller 5 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
