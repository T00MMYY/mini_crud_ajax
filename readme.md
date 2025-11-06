# Cómo funciona el botón “Editar”

El botón Editar permite modificar un usuario sin recargar la página.

Cada fila de la tabla tiene un botón “Editar” con un atributo data-posicion que indica el índice del usuario en la lista.

Detectar el clic: Se usa un eventListener en la tabla que detecta cuándo se hace clic en un botón “Editar”.

Cargar datos en el formulario:

Se obtienen los datos del usuario desde la lista.

Se rellenan los campos del formulario con esos datos.

Se cambia el botón a “Actualizar usuario” y el título del formulario a “Editar usuario”.

Guardar cambios: Al enviar el formulario, los datos actualizados se envían al servidor y la tabla se refresca automáticamente.

https://github.com/T00MMYY/mini_crud_ajax.git
