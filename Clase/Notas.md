# 🗒️ Registro de Trabajo en Clase - Taller X

## 📆 Fecha de la sesión
19/09/2025  


---

## 👥 Integrantes presentes
- Juan Andrés Lacouture Daza


---

## 🧠 Actividades realizadas en clase
Durante la sesión se seleccionó el flujo **“Gestión de Roles: Estudiante, Docente, Administrador”** de la plataforma EdukIT para aplicar el marco STRIDE.  

**Actividades principales:**
- Análisis del flujo de gestión de roles y sus implicaciones de seguridad.
- Discusión sobre amenazas críticas en este contexto (suplantación, alteración y escalada de privilegios).
- Construcción de la tabla preliminar en Excel (`tabla-strideclase.xlsx`) con amenazas, impactos, mitigaciones y responsables.
- Reflexión sobre por qué este flujo es el más crítico en términos de seguridad.

---

## 🧩 Boceto inicial del modelo
Se creó un primer borrador de la tabla STRIDE en Excel con los seis tipos de amenazas aplicados al flujo de roles.  


---

## 📑 Justificación de la elección del flujo
El flujo de **gestión de roles** es el núcleo de la seguridad en EdukIT.  
- Los **Estudiantes** solo deben acceder a sus propios cursos y calificaciones.  
- Los **Docentes** pueden modificar y publicar contenidos, pero no administrar usuarios.  
- Los **Administradores** controlan privilegios y políticas globales.  

**Justificación:** Si este flujo falla, se comprometen los tres principios básicos de seguridad:  
- **Integridad** (alteración indebida de roles o permisos).  
- **Confidencialidad** (exposición de información sensible).  
- **Disponibilidad** (servicio inaccesible ante ataques).  

Esto lo convierte en el flujo más crítico para aplicar STRIDE en EdukIT.

---

## 📊 Tabla STRIDE – Flujo: Roles (Estudiante, Docente, Administrador)

## Spoofing (Suplantación)
**Amenaza:** Un atacante se hace pasar por un Docente usando credenciales robadas para alterar permisos o gestionar cursos.  
**Impacto:** Acceso no autorizado a funciones docentes, modificación indebida de calificaciones o contenidos.  
**Mitigación:** Autenticación multifactor (MFA), detección de anomalías, monitoreo de intentos fallidos, rotación de credenciales.  

**Justificación:** En la gestión de roles, la suplantación es crítica porque permite a un atacante **elevarse automáticamente a un rol con más privilegios**. Un Estudiante suplantando a un Docente podría alterar notas, y alguien suplantando a un Administrador podría reconfigurar todo el sistema. MFA y monitoreo de login son medidas estándar porque **reducen drásticamente la probabilidad de éxito de ataques de credential stuffing o phishing**.

---

## Tampering (Alteración)
**Amenaza:** Un Estudiante manipula su sesión/token para intentar elevar su rol a Docente o Administrador.  
**Impacto:** Alteración de la integridad del sistema de roles y acceso indebido a privilegios superiores.  
**Mitigación:** Validación en servidor de tokens, controles RBAC/ABAC, auditoría inmutable, verificaciones de integridad.  

**Justificación:** En este flujo, los tokens y ACLs son **la llave de acceso**. Si un Estudiante puede manipularlos desde el cliente, compromete la **integridad del modelo de roles**. Por eso, las validaciones deben estar **siempre del lado del servidor**, y los cambios deben dejar rastro en una bitácora inmutable, asegurando que **ningún rol se cambie sin control ni evidencia**.

---

## Repudiation (Negación de acción)
**Amenaza:** Un Administrador niega haber cambiado el rol de un Estudiante a Docente.  
**Impacto:** Pérdida de trazabilidad y dificultad para sancionar o corregir abusos de privilegios.  
**Mitigación:** Logs con firma digital, sellos de tiempo, registros detallados de cambios de rol, acceso segregado a bitácoras.  

**Justificación:** La gestión de roles requiere **responsabilidad y trazabilidad absoluta**. Sin logs confiables, un Administrador podría negar cambios indebidos y no habría forma de comprobarlo. Los registros con firma digital y sellado de tiempo garantizan que las acciones sean **irrefutables**, lo que evita la negación de responsabilidades.

---

## Information Disclosure (Divulgación de información)
**Amenaza:** Un Estudiante accede a información reservada de roles de Docente o Administrador por mala configuración de permisos.  
**Impacto:** Exposición de información sensible (datos de docentes, configuraciones administrativas).  
**Mitigación:** Control de acceso granular, revisiones periódicas de permisos, cifrado en tránsito y reposo, pruebas de acceso cruzado.  

**Justificación:** Una mala configuración de permisos en el módulo de roles podría dar a un Estudiante acceso a **información crítica** como configuraciones administrativas, listas de usuarios o datos de Docentes. Esta amenaza es relevante porque compromete la **confidencialidad**. La mitigación con controles de acceso y revisiones periódicas asegura que solo cada rol vea **exactamente lo que le corresponde**.

---

## Denial of Service (Denegación de servicio)
**Amenaza:** Un atacante genera múltiples solicitudes de cambio de rol para saturar el servicio de administración de usuarios.  
**Impacto:** Indisponibilidad del servicio de roles, retrasos en la operación académica.  
**Mitigación:** WAF y rate limiting, autenticación fuerte para cambios de rol, autoescalado en la nube, alertas de saturación.  

**Justificación:** Si el sistema de roles queda indisponible, **nadie puede autenticarse correctamente ni modificar privilegios**, lo que bloquea el funcionamiento de EdukIT. Aunque no expone información, el DoS compromete la **disponibilidad**, que es uno de los tres pilares de seguridad. Los límites de velocidad y escalado automático son esenciales porque evitan que un ataque simple degrade todo el sistema.

---

## Elevation of Privilege (Escalada de privilegios)
**Amenaza:** Un Estudiante explota un error en la gestión de roles para convertirse en Administrador.  
**Impacto:** Acceso total al sistema, modificación de datos críticos y control de la plataforma.  
**Mitigación:** Principio de mínimo privilegio, revisiones de código, pruebas de penetración, aprobación múltiple en cambios críticos de rol.  

**Justificación:** Esta es la amenaza más grave en el flujo de roles. Si un Estudiante logra escalar a Administrador, tiene **control absoluto** sobre EdukIT: puede asignar privilegios, modificar notas, y exfiltrar datos. El principio de mínimo privilegio y las pruebas de penetración aseguran que solo los usuarios autorizados mantengan control, y la **doble aprobación** agrega una capa adicional que dificulta el abuso de privilegios.

---

## 🔁 Tareas definidas para complementar el taller

| Tarea asignada                  | Responsable              | Fecha estimada |
|---------------------------------|--------------------------|----------------|
| Completar y depurar tabla STRIDE en Excel | Juan Andrés Lacouture Daza | 20/09 |
| Redacción del informe final      | Juan Andrés Lacouture Daza | 21/09 |
| Investigación de buenas prácticas | Juan Andrés Lacouture Daza | 21/09 |


---

_Este documento integra el registro de trabajo en clase y la justificación detallada de la tabla STRIDE aplicada al flujo de gestión de roles en EdukIT._
