# Auditoría · Versión A

**Código:** e7371  
**Repositorio público propio:** [Agregar enlace de GitHub]  
**Rama:** examen/e7371

## A-01 · No se registra el avistamiento

**Síntoma:** Al intentar registrar un avistamiento, el formulario no completaba correctamente el guardado.

**Causa:** En `FormularioAvistamiento.tsx`, el frontend enviaba `criaturaId`, mientras que el backend esperaba el campo `criatura`.

**Cambio:** Se reemplazó la asignación condicional por `datos.criatura = form.criatura`, para mantener el mismo nombre de campo en el frontend y backend.

**Pruebas:** Se registró un avistamiento correctamente, obteniendo HTTP 201. El detalle se abrió y las consultas posteriores devolvieron HTTP 200.

**Estado:** Corrección funcionando. Falta evidencia de la prueba con referencia inexistente (HTTP 404) y confirmación explícita de persistencia después de recargar.

## A-02 · La lista no identifica a la criatura

**Síntoma:** Los avistamientos mostraban el ID de la criatura en lugar de su nombre.

**Causa:** La función `listar()` de `avistamientos.service.ts` no utilizaba `populate()`, por lo que solamente devolvía la referencia de MongoDB.

**Cambio:** Se agregó `.populate('criatura', 'nombre')` para obtener también el nombre de cada criatura.

**Pruebas:** Se comprobó que el listado muestra correctamente los nombres de las criaturas asociadas y que las solicitudes GET responden HTTP 200.

**Estado:** Corrección funcionando. Falta comprobar una consulta sin resultados.

## A-03 · Se acepta un peligro inválido

**Síntoma:** La API permitía actualizar una criatura con niveles de peligro fuera del rango permitido de 1 a 10.

**Causa:** La función `actualizar()` de `criaturas.service.ts` utilizaba `findByIdAndUpdate()` sin activar las validaciones del esquema.

**Cambio:** Se agregó `runValidators: true` para validar los datos durante las actualizaciones.

**Pruebas:** Se utilizó PowerShell para actualizar el nivel de peligro de Valdur a 7, obteniendo HTTP 200. Después se intentó actualizar a 999 y la API respondió HTTP 400, rechazando el valor inválido.

**Estado:** Validación funcionando. Falta documentar el GET posterior para confirmar que se conserva el nivel 7.

## A-04 · El filtro no actualiza la pantalla

**Síntoma:** Al seleccionar otro tipo de criatura, el filtro cambiaba, pero los resultados no se actualizaban automáticamente.

**Causa:** El `useEffect` de `ListaCriaturas.tsx` dependía solamente de `recarga`, por lo que no detectaba los cambios de `tipo`.

**Cambio:** Se agregó `tipo` al arreglo de dependencias del efecto, quedando `[tipo, recarga]`.

**Pruebas:** Se comprobó que las consultas GET de criaturas responden HTTP 200 y que el listado general carga correctamente. Se implementó la actualización automática del filtro.

**Estado:** Corrección implementada. Falta dejar evidencia de los cambios entre `mitica`, `mecanica` y `Todos`, además de los estados de carga, error y lista vacía.