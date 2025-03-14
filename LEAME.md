<p align="center">
    <a href="https://mylisterhub.com" target="_blank">
        <img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/logo.svg" width="75" alt="Logo" style="padding-right: 5px;">
        <img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/company.svg" width="400" alt="MyListerHub" style="padding-bottom: 2px;">
    </a>
</p>

<p align="center">
    <a href="https://github.com/FmTod/">Guidelines</a>
</p>

<p align="center">
    <a href="https://forms.gle/gSqn6SE3Wa65b3bS7">Questionnaire</a>
</p>

<p align="center">
    <a href="./README.md">Inglés / English</a>
</p>

# Evaluación

Paquete de Interacción con la API de Citas con Limitación de Tasa, Caché y UI en Vue.js

## Objetivo

Evaluar tu capacidad para diseñar, desarrollar, probar y documentar un paquete integral de Laravel que consuma datos de citas de la API `https://dummyjson.com/quotes`, implemente limitación de tasa de solicitudes, utilice caché local con recuperación eficiente usando búsqueda binaria, y proporcione una interfaz de usuario preconstruida y publicable con Vue.js para interactuar con la API.

## Tarea

Desarrollar un paquete de Laravel que simplifique la interacción con la API pública `https://dummyjson.com/quotes`. El paquete debe incluir interacción con la API, limitación de tasa, caché y una interfaz de usuario construida con Vue.js para mostrar las citas. Los artefactos de construcción de la UI deben ser publicables para su personalización.

**Tiempo Asignado:** 8 - 12 horas

## Entregables

* Un enlace a un repositorio Git que contenga el código completo del paquete de Laravel.
* Un archivo `README.md` en el directorio raíz del paquete con instrucciones claras para la instalación, configuración, uso básico, limitación de tasa, caché y acceso/publicación de la UI en Vue.js.

## Requisitos

1. **Estructura del Paquete:**
    * Sigue las convenciones estándar de desarrollo de paquetes de Laravel.
    * Incluye un proveedor de servicios para registrar la funcionalidad del paquete, rutas y activos publicables.
    * Incluye la estructura de directorios necesaria para tu aplicación Vue.js (por ejemplo, `resources/js`, `resources/views`).

2. **Servicio Cliente de API:**
    * Crea un servicio dentro del paquete que maneje la comunicación con la API `https://dummyjson.com/quotes` usando el cliente HTTP de Laravel.
    * Este servicio debe incorporar lógica de limitación de tasa de solicitudes y caché local con búsqueda binaria.

3. **Configuración:**
    * Proporciona un archivo de configuración para el paquete (por ejemplo, `config/quotes.php`).
    * El archivo de configuración debe permitir a los usuarios definir:
        * La URL base de la API (por defecto `https://dummyjson.com`).
        * El número máximo de solicitudes permitidas por ventana de tiempo (por ejemplo, por minuto).
        * La duración de la ventana de tiempo en segundos (por ejemplo, 60 para un minuto).

4. **Métodos de Interacción con la API:**
    * `getAllQuotes()`: Obtiene todas las citas del endpoint `/quotes`.
    * `getRandomQuote()`: Obtiene una cita aleatoria del endpoint `/quotes/random`.
    * `getQuote(int $id)`: Obtiene una cita específica por su ID del endpoint `/quotes/{id}`. Este método debe primero verificar el caché local usando búsqueda binaria.

5. **Implementación de Limitación de Tasa:**
    * Implementa un mecanismo para rastrear el número de solicitudes hechas a la API dentro de la ventana de tiempo configurada.
    * Si se excede el límite, pausa la ejecución por un corto período hasta que la ventana se reinicie y luego reintenta la solicitud.

6. **Caché Local con Recuperación Eficiente:**
    * Implementa un mecanismo de caché local (por ejemplo, un array) para almacenar las citas obtenidas.
    * El método `getQuote(int $id)` debe primero verificar este caché.
    * Si la cita con el ID dado se encuentra en el caché, recupérala usando búsqueda binaria (asumiendo que los datos en caché están ordenados por ID) y devuélvela sin hacer una llamada a la API.
    * Si la cita no está en el caché, haz una llamada a la API, almacena la cita obtenida en el caché (asegurando que el caché permanezca ordenado por ID para la búsqueda binaria) y luego devuélvela.

7. **Interfaz de Usuario en Vue.js:**
    * Construye una interfaz de usuario usando Vue.js dentro de tu paquete. Esta UI debe permitir a los usuarios:
        * Ver todas las citas (potencialmente con paginación).
        * Ver una cita aleatoria.
        * Ver una cita específica por ID.
    * Esta UI debe hacer solicitudes a la API de tu paquete para obtener los datos.

8. **Rutas de la API del Paquete:**
    * Define rutas de API dentro de tu paquete (registradas a través del proveedor de servicios, probablemente bajo un prefijo `/api/quotes`) que tu aplicación Vue.js pueda consumir. Estas rutas deben:
        * `/api/quotes`: Devolver todas las citas.
        * `/api/quotes/random`: Devolver una cita aleatoria.
        * `/api/quotes/{id}`: Devolver una cita específica por ID.
    * Crea controlador(es) dentro de tu paquete para manejar estas rutas de API e interactuar con tu servicio cliente de API.

9. **Servir la Aplicación Vue.js:**
    * Define una ruta en tu paquete (por ejemplo, `/quotes-ui`) que sirva el punto de entrada principal de tu aplicación Vue.js. Necesitarás configurar Vite dentro de tu paquete para construir la aplicación Vue.js en activos estáticos.

10. **Activos Publicables:**
    * Configura el proveedor de servicios de tu paquete para hacer que los activos construidos de la aplicación Vue.js (por ejemplo, la carpeta `dist` que contiene JavaScript y CSS) sean publicables en la aplicación principal de Laravel usando `php artisan vendor:publish`. Los activos publicados deben residir en un directorio lógico dentro del directorio `public` de la aplicación principal (por ejemplo, `public/vendor/your-package-name`).

11. **Uso:**
    * Incluye instrucciones sobre cómo instalar el paquete, configurarlo y cómo acceder a la UI preconstruida de Vue.js (la ruta definida, por ejemplo, `/quotes-ui`).
    * Proporciona instrucciones claras sobre cómo publicar los activos de la UI de Vue.js si un desarrollador desea personalizar el frontend. Incluye pasos sobre dónde se publican los activos y cómo pueden ser modificados.

12. **Pruebas:**
    * Incluye pruebas unitarias para el servicio cliente de API.
    * Incluye pruebas básicas de características para las rutas de la API de tu paquete para asegurar que devuelvan los datos correctos.

13. **Documentación:**
    * El `README.md` debe incluir documentación completa para todas las características, incluyendo instrucciones claras sobre cómo acceder y publicar la UI de Vue.js y cualquier paso de construcción necesario (por ejemplo, ejecutar `npm install` y `npm run build` dentro del directorio de la UI del paquete).

## Instrucciones de Envío

1. Crea un nuevo repositorio privado en una plataforma como GitHub, GitLab o Bitbucket.
2. Desarrolla el paquete de Laravel según los requisitos descritos anteriormente.
3. Asegúrate de que todas las pruebas pasen y la documentación esté completa.
4. Otorga acceso a tu repositorio a los evaluadores designados.
5. Envía el enlace del repositorio a los evaluadores designados.

¡Buena suerte!