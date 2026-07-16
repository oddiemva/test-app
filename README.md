# Quiz CLI

Aplicación interactiva de línea de comandos construida con Node.js para evaluar conocimientos de programación mediante cuestionarios por categorías. El repositorio contiene una implementación sencilla orientada a consola, con preguntas almacenadas en un archivo JSON y lógica modular separada para entrada de usuario, presentación visual y flujo del juego.

## Descripción general

Este proyecto resuelve un caso de uso educativo: ejecutar quizzes desde terminal sin dependencias externas. La aplicación permite al usuario:

- seleccionar una categoría de preguntas;
- elegir cuántas preguntas responder;
- contestar cada pregunta desde la terminal;
- recibir retroalimentación inmediata;
- ver un resumen final con puntuación y revisión de respuestas incorrectas;
- reiniciar la experiencia para volver a jugar.

A partir del código fuente, se identificó que el proyecto también funciona como ejemplo didáctico de características modernas de JavaScript y Node.js, incluyendo ES Modules, `async/await`, lectura de archivos JSON, manejo de entrada por consola y programación orientada a objetos.

## Características

- Interfaz interactiva en terminal.
- Selección de categoría de preguntas.
- Selección de cantidad de preguntas (`All questions`, `3 questions`, `5 questions`, según disponibilidad).
- Carga de preguntas desde `data/questions.json`.
- Orden aleatorio de preguntas mediante el algoritmo Fisher-Yates.
- Validación de entrada del usuario para opciones numéricas.
- Retroalimentación inmediata sobre respuestas correctas e incorrectas.
- Barra de progreso durante el quiz.
- Resumen final con porcentaje de aciertos.
- Revisión de preguntas incorrectas al finalizar.
- Posibilidad de jugar nuevamente sin reiniciar manualmente el proceso.
- Salida coloreada mediante códigos ANSI sin librerías externas.

## Tecnologías utilizadas

### Lenguajes

- JavaScript (ES Modules)
- JSON

### Runtime

- Node.js `>=18.0.0`

### APIs y módulos utilizados

Todos los módulos identificados son nativos de Node.js:

- `node:fs/promises` para lectura asíncrona del archivo de preguntas.
- `node:path` para resolver rutas de archivos.
- `node:url` para obtener la ruta del módulo actual en entorno ES Modules.
- `node:readline` para interacción por consola.

### Dependencias

No se identificaron dependencias externas en `package.json`.

### Herramientas

- npm para ejecución de scripts.
- Node.js Test Runner configurado mediante el script `node --test`.

## Arquitectura

La arquitectura identificada es la de una aplicación CLI monolítica, modularizada por responsabilidades:

- **Entrada principal (`index.js`)**: inicializa la aplicación, carga preguntas, coordina el flujo del juego y maneja errores.
- **Módulo de entrada (`src/input.js`)**: abstrae el uso de `readline` para preguntar, confirmar y seleccionar opciones.
- **Lógica de dominio (`src/quiz.js`)**: implementa la clase `Quiz`, el progreso, el puntaje, la evaluación de respuestas y la visualización de resultados.
- **Presentación (`src/colors.js`)**: encapsula estilos ANSI para mejorar la salida en terminal.
- **Datos (`data/questions.json`)**: almacena categorías, preguntas, opciones, respuesta correcta y explicación.

### Flujo general

1. La aplicación inicia desde `index.js`.
2. Se cargan las preguntas desde `data/questions.json`.
3. El usuario selecciona una categoría.
4. El usuario elige la cantidad de preguntas disponibles para esa categoría.
5. Se instancia `Quiz` con las preguntas seleccionadas.
6. Cada pregunta se presenta por consola y se registra la respuesta.
7. Se muestra retroalimentación inmediata y explicación.
8. Al finalizar, se imprime el resultado general y la revisión de errores.
9. El usuario decide si desea volver a jugar.

## Estructura del proyecto

```text
.
├── README.md
└── test-app/
    └── test-app/
        ├── index.js              # Punto de entrada de la aplicación CLI
        ├── package.json          # Metadatos del proyecto y scripts npm
        ├── data/
        │   └── questions.json    # Banco de preguntas y categorías
        └── src/
            ├── colors.js         # Utilidades para colorear la salida en terminal
            ├── input.js          # Manejo de entrada interactiva con readline
            └── quiz.js           # Clase principal del quiz y resultados
```

> La aplicación fuente se encuentra dentro de `test-app/test-app`, no en la raíz del repositorio.

## Requisitos previos

- Node.js `>=18.0.0`
- npm
- Una terminal compatible con salida ANSI para visualizar colores correctamente

## Instalación

1. Clona el repositorio:

   ```bash
   git clone https://github.com/oddiemva/test-app.git
   ```

2. Entra al directorio de la aplicación:

   ```bash
   cd test-app/test-app/test-app
   ```

3. Instala dependencias:

   ```bash
   npm install
   ```

> No se identificaron dependencias de terceros, pero `npm install` permite preparar el proyecto de acuerdo con `package.json`.

## Configuración

### Variables de entorno

No se encontraron archivos `.env`, `.env.example` ni referencias a variables de entorno en el código fuente analizado.

### Archivos de configuración

- `package.json`: define nombre, versión, scripts, licencia y versión mínima de Node.js.
- `data/questions.json`: archivo de contenido con categorías y preguntas del quiz.

### Parámetros importantes

No se identificaron parámetros CLI, flags ni archivos de configuración adicionales.

## Ejecución

Desde el directorio `test-app/test-app` puedes iniciar la aplicación con cualquiera de estos comandos:

```bash
npm start
```

O directamente con Node.js:

```bash
node index.js
```

## Ejemplos de uso

### Flujo esperado en consola

1. Se muestra un banner de bienvenida.
2. Se listan las categorías disponibles:
   - JavaScript Basics
   - Node.js Fundamentals
   - General Programming
3. Se solicita el número de preguntas.
4. Se responde cada pregunta introduciendo el número de la opción.
5. Se muestra el resultado final con puntaje y recomendaciones.

### Ejemplo de interacción

```text
Choose a category:

  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming

Your choice (enter number): 1
```

```text
How many questions?

  1. All questions
  2. 3 questions
  3. 5 questions

Your choice (enter number): 2
```

## Scripts disponibles

Los scripts definidos en `package.json` son:

| Script | Comando | Descripción |
|---|---|---|
| `start` | `node index.js` | Inicia la aplicación interactiva del quiz. |
| `test` | `node --test` | Ejecuta el runner de pruebas nativo de Node.js. |

## Pruebas

El proyecto define el siguiente comando de prueba:

```bash
npm test
```

No se encontraron archivos de prueba ni directorios de tests en el repositorio analizado. Por lo tanto, no se pudo determinar a partir del código fuente qué cobertura de pruebas existe realmente.

## Despliegue

No se encontraron archivos ni configuraciones de despliegue como `Dockerfile`, `docker-compose.yml`, workflows de GitHub Actions, infraestructura como código o scripts de publicación.

No se pudo determinar a partir del código fuente un proceso formal de despliegue. El proyecto parece estar pensado para ejecución local en terminal.

## Datos del cuestionario

El banco de preguntas actual está organizado en tres categorías:

- **JavaScript Basics**
- **Node.js Fundamentals**
- **General Programming**

Cada pregunta contiene:

- enunciado;
- lista de opciones;
- índice de la respuesta correcta;
- explicación mostrada tras responder.

## Contribución

No se encontró una guía formal de contribución (`CONTRIBUTING.md`). A partir de la estructura del proyecto, una contribución razonable podría seguir este flujo:

1. Crear una rama de trabajo.
2. Realizar cambios en la lógica, preguntas o experiencia CLI.
3. Ejecutar la aplicación localmente.
4. Ejecutar `npm test`.
5. Abrir un Pull Request.

Si se agregan nuevas preguntas, deben mantener la estructura actual de `data/questions.json`.

## Licencia

El archivo `package.json` declara licencia **MIT**.

No se encontró un archivo `LICENSE` separado en el repositorio analizado.

## Autoría

No se pudo determinar a partir del código fuente quién es el autor o mantenedor del proyecto.
