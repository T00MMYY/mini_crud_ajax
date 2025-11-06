# Botón Editar

Este proyecto implementa un CRUD de usuarios utilizando JavaScript puro y AJAX, sin librerías externas. Esta guía se centra en cómo funciona el botón “Editar”, paso a paso.

📌 Objetivo del botón Editar

El botón “Editar” permite modificar un usuario existente en la tabla, rellenando el formulario con sus datos actuales, sin recargar la página, y actualizando la tabla automáticamente al guardar los cambios.

🛠 Implementación
1️⃣ Renderizado del botón en la tabla

Cuando se construye la tabla de usuarios (renderizarTablaDeUsuarios), cada fila incluye un botón “Editar”:

<button
  type="button"
  class="boton-editar"
  data-posicion="0"
  aria-label="Editar usuario 1">
  Editar
</button>


class="boton-editar": Permite identificar el botón.

data-posicion: Guarda el índice del usuario en la lista.

aria-label: Mejora accesibilidad.

2️⃣ Captura del evento de clic

Se usa un listener global en el <tbody> de la tabla:

nodoCuerpoTablaUsuarios?.addEventListener('click', async (evento) => {
    const nodoBoton = evento.target.closest('button[data-posicion]');
    if (!nodoBoton) return;
});


Se detecta si el clic fue sobre un botón con data-posicion.

Esto permite capturar el clic sin asignar un listener a cada botón individual.

3️⃣ Obtener los datos del usuario

Al hacer clic en “Editar”, se solicita la lista de usuarios al servidor:

const respuestaHttp = await fetch(`${URL_API_SERVIDOR}?action=list`);
const cuerpoJson = await respuestaHttp.json();
const usuarioAEditar = cuerpoJson.data[posicionUsuario];


Se obtiene el usuario correspondiente según su posición en la lista.

Esto asegura que siempre se edite la información más actual.

4️⃣ Activar modo edición

Se llama a la función activarModoEdicion pasando el índice y los datos del usuario:

activarModoEdicion(posicionUsuario, usuarioAEditar);


Dentro de esta función:

Se activa una bandera modoEdicion = true.

Se guarda el índice del usuario en edición indiceUsuarioEnEdicion = posicionUsuario.

Se rellenan los campos del formulario con los datos del usuario:

campoNombre.value = datosUsuario.nombre || '';
campoEmail.value = datosUsuario.email || '';


Se cambia el texto del botón a “Actualizar usuario”.

Se cambia el título del formulario a “Editar usuario”.

Se hace scroll al formulario para que sea visible:

formularioAltaUsuario?.scrollIntoView({ behavior: 'smooth' });

5️⃣ Guardar cambios

Cuando se envía el formulario en modo edición:

if (modoEdicion) {
    url = `${URL_API_SERVIDOR}?action=update`;
    datosUsuario.index = indiceUsuarioEnEdicion;
}


Se envía un POST a la API con el índice del usuario y los nuevos datos.

Se actualiza automáticamente la tabla con renderizarTablaDeUsuarios.

Se desactiva el modo edición y se restaura el formulario a su estado normal.

6️⃣ Flujo resumido

Usuario hace clic en “Editar”.

Se identifica el usuario mediante data-posicion.

Se obtienen los datos actuales desde la API.

Se rellena el formulario y se activa el modo edición.

Usuario modifica los datos y envía el formulario.

Se envían los datos actualizados a la API y se refresca la tabla.

✅ Beneficios de este enfoque

Sin recargar la página.

Siempre muestra datos actualizados.

Fácil de mantener y ampliar.

Evita errores al usar data-posicion y fetch.