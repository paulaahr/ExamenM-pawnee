# Uso de IA

**Herramientas utilizadas:** ChatGPT (OpenAI).

**Solicitudes representativas:**
- Revisar los errores de la aplicación MERN de Pawnee e identificar sus posibles causas.
- Ayudar a corregir los problemas de validación, referencias de MongoDB y actualización de estados en React.

**Decisión técnica:** Utilicé las sugerencias de IA como apoyo para identificar los errores. Apliqué las correcciones que correspondían al funcionamiento de la aplicación, como el uso de `populate()`, `runValidators: true` y las dependencias de `useEffect`. También revisé que los cambios respetaran la estructura original del proyecto y no eliminaran las validaciones existentes.

**Cómo verifiqué los cambios:** Realicé pruebas desde la aplicación y las herramientas de desarrollador del navegador, revisando las solicitudes HTTP. También utilicé PowerShell para comprobar que la API aceptara un nivel de peligro válido con HTTP 200 y rechazara el valor 999 con HTTP 400. Verifiqué además el registro de avistamientos con HTTP 201 y la visualización de los nombres de las criaturas.