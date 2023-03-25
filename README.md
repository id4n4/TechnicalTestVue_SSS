# Prueba técnica desarrollador front-end

Se requiere desarrollar un formulario de registro con los Vue.js y Tailwind
Requerimientos

1.  El formulario debe de tener 3 pasos, con la posibilidad de avanzar y retroceder entre ellos, previa validación de los campos obligatorios

2. El formulario debe tener una línea de tiempo que indique en que paso se encuentra actualmente.

3. El formulario debe tener los siguientes campos:
  - **Paso 1**
    - País
      * Este debe ser de tipo Select y deberá mostrar lista de países descargada por internet.
    - Genero
    - Primer nombre
    - Segundo nombre
    - Fecha de nacimiento
      * Este deberá desplegar un calendario donde se pueda seleccionar la fecha (YYYY - MM – DD) y validar que según la fecha no tenga menos de 18 años
    - Tipo documento
      * Este debe ser de tipo Select con las opciones: Cedula de ciudadanía, Pasaporte y Cedula de extranjería
    - Numero documento
      * Este debe de permitir solo dígitos numéricos y no tener menos de 5dígitos
    - Foto documento – Frente
      * Este debe de permitir cargar un archivo JPG
    - Foto documento – Reverso
      * Este debe de permitir cargar un archivo JPG
      
  - **Paso 2**
    - Correo electrónico
      * Validar que lo ingresado tenga formato de correo
    - Contraseña
    - Confirmación de Contraseña
      * Validar que sea igual a la contraseña
    - Numero teléfono
    - Numero celular
    
  - **Paso 3**
    - Dirección residencia
    - Código postal

4. En el Paso 3 al accionar el botón para enviar el formulario, este debe de imprimir en la consola el valor de cada campo y mostrar en la vista un modal confirmando que este fue enviado con éxito
   
5. Los campos deben ser validados a medida que son ingresados y si es correcto mostrar un icono de CHECK sino una X, junto a cada campo
    
## Información adicional
Todos los campos son obligatorios para poder avanzar al siguiente paso
electrónico
