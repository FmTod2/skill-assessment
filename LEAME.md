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

# Evaluación de Habilidades: Paquete Laravel y Arquitectura

## Objetivo

Evaluar su capacidad para diseñar un paquete Laravel modular y escalable. Buscamos **arquitectura limpia**, **familiaridad con el ecosistema** (Service Providers, Facades), **resolución de problemas algorítmicos** y **automatización de infraestructura**.

## La Tarea

Desarrollar un paquete de Laravel que interactúe con la API `https://dummyjson.com/quotes`. El paquete debe servir como un puente para obtener, almacenar en caché y mostrar citas a través de una interfaz de usuario Vue.js, respetando estrictamente los límites de velocidad (rate limits) de la API.

## Restricciones de Entrega

> [!WARNING]
> **Lea Atentamente:** El incumplimiento de estas restricciones resultará en descalificación inmediata.
> 1. **Estructura:** El repositorio debe contener **únicamente** el código del Paquete Laravel. No envíe una Aplicación Laravel completa.
> 2. **Sin IA:** Esta tarea debe completarse **enteramente sin la ayuda de asistentes de IA** (Copilot, ChatGPT, etc.).
> 3. **Completitud:** Todos los requisitos deben ser funcionales dentro del entorno Docker proporcionado.

## Requisitos

### 1. Arquitectura del Paquete

* Seguir las convenciones estándar de paquetes Laravel (Service Provider, Facades, publicación de configuración).
* **Bonus:** Se permite y fomenta el uso de bibliotecas modernas del ecosistema (ej. **Saloon** para integraciones API).

### 2. Servicio API y Rate Limiting

* Crear una clase de servicio para comunicarse con `https://dummyjson.com/quotes`.
* **Configuración:** Los usuarios deben poder definir `base_url`, `request_limit` (ej. 5) y `time_window` (ej. 30 segundos) a través de un archivo de configuración publicado.
* **Restricción:** El Servicio **no debe** dormir ni esperar (`sleep`/`wait`). Si se excede el límite de velocidad, debe lanzar una excepción personalizada `RateLimitExceededException`.
* **Persistencia:** Utilizar un driver de caché para almacenar el conteo de peticiones, asegurando que los límites persistan entre diferentes solicitudes.

### 3. Caché y Restricción Algorítmica

* **Restricción:** Debe implementar una estrategia de caché personalizada para el método `getQuote(int $id)`.
* **Almacenamiento:** Guardar las citas obtenidas en la caché como un **array plano, indexado numéricamente** y ordenado por ID (ej. `[{id: 1...}, {id: 5...}]`). **No** utilice el ID como clave del array asociativo.
* **Recuperación:** Cuando se llame a `getQuote($id)`:
    1. Recuperar la lista completa de la caché.
    2. **Implementar un algoritmo de Búsqueda Binaria** para encontrar la cita con el ID correspondiente dentro de la lista.
    3. Si se encuentra, devolverla.
    4. Si no se encuentra, obtenerla de la API, reordenar la lista, actualizar la caché y devolver el resultado.


* *Nota: Somos conscientes de que esta no es la estrategia más eficiente en PHP. Estamos evaluando su capacidad para implementar algoritmos y manipular estructuras de datos.*

### 4. Comando de Importación Inteligente (Resolución de Problemas)

* Crear un comando de consola: `php artisan quotes:batch-import {count}`.
* **Objetivo:** Obtener `{count}` citas *únicas* y almacenarlas en la caché.
* **Lógica:**
    * El comando debe capturar la excepción `RateLimitExceededException` de su servicio y **dormir/esperar** hasta que la ventana de tiempo se reinicie, y luego reintentar automáticamente.
    * Debe garantizar la unicidad (descartar duplicados encontrados en la API que ya existan en la caché).
    * Proporcionar retroalimentación en tiempo real en la terminal (ej. "Obtenidas 5/20... Límite alcanzado, esperando 30s...").



### 5. Interfaz de Usuario Vue.js

* Construir una UI utilizando **Vue.js (Composition API + TypeScript)**.
* **Características:**
    * Ver todas las citas (Paginadas).
    * Ver una sola cita por ID (debe utilizar la lógica de Búsqueda Binaria del backend).


* **Integración:**
* Registrar una ruta web (ej. `/quotes-ui`) en el paquete para servir la SPA.
* Configurar Vite para compilar los assets en una carpeta `dist/` dentro del paquete.
* Asegurar que los assets puedan publicarse en una aplicación anfitriona mediante `vendor:publish`.



### 6. Infraestructura (Docker)

* **Requisito:** El repositorio debe estar limpio (solo archivos del paquete), pero debe proporcionar un `docker-compose.yml` (y `Dockerfile`) que construya un entorno de prueba funcional.
* **El Proceso de Construcción:**
    * El contenedor debe instalar automáticamente una aplicación Laravel fresca (nueva).
    * Debe copiar el código de su paquete dentro del contenedor.
    * Debe enlazar/instalar el paquete dentro de la aplicación Laravel fresca (ej. usando repositorios `path` de Composer).


* **Objetivo:** El evaluador debe poder clonar su repositorio, ejecutar `docker-compose up`, visitar `localhost:8080/quotes-ui` y ver la aplicación funcionando sin pasos de instalación manuales.

### 7. Pruebas (Testing)

* **Pruebas Unitarias:** Probar el algoritmo de Búsqueda Binaria de forma aislada.
* **Pruebas de Funcionalidad (Feature Tests):** Probar los endpoints de la API y el Comando de Consola (simulando/mocking la API para replicar los límites de velocidad).
* **Herramienta:** Las pruebas deben escribirse utilizando **PestPHP**.

## Entregables

1. Enlace al Repositorio Git público.
2. Archivo `README.md` con:
    * Guía de instalación.
    * Explicación de su estrategia de Rate Limiting.
    * Instrucciones para ejecutar el entorno Docker.

¡Buena suerte!
