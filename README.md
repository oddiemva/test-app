# Quiz CLI

Aplicación de línea de comandos desarrollada con Node.js para ejecutar un cuestionario interactivo sobre programación. El proyecto carga preguntas desde un archivo JSON, permite seleccionar una categoría y la cantidad de preguntas a responder, evalúa cada respuesta en tiempo real y muestra un resumen final con la puntuación obtenida.

## Descripción general

Este repositorio contiene una aplicación educativa orientada a terminal. Su propósito es ofrecer un quiz interactivo para practicar conceptos de programación y, al mismo tiempo, servir como ejemplo sencillo de una aplicación Node.js estructurada por módulos.

A partir del código fuente se identificó que la aplicación:

- carga preguntas desde un archivo local JSON;
- organiza el contenido por categorías;
- permite al usuario elegir categoría y cantidad de preguntas;
- presenta preguntas de opción múltiple por consola;
- valida respuestas y muestra retroalimentación inmediata;
- imprime un resultado final con porcentaje de aciertos;
- permite reiniciar la experiencia para volver a jugar.

También funciona como ejemplo de uso de características modernas de JavaScript y Node.js, incluyendo ES Modules, `async/await`, lectura de archivos con `fs/promises`, manejo de entrada estándar con `readline` y encapsulación de lógica mediante clases.

## Características

- Interfaz interactiva en terminal.
- Selección de categoría de preguntas.
- Selección del número de preguntas según disponibilidad.
- Preguntas de opción múltiple.
- Carga de datos desde `data/questions.json`.
- Mezcla aleatoria de preguntas usando Fisher-Yates.
- Validación de entrada numérica del usuario.
- Feedback inmediato sobre respuestas correctas e incorrectas.
- Explicaciones asociadas a cada pregunta.
- Barra de progreso durante la partida.
- Resumen final con puntuación y porcentaje.
- Revisión de respuestas incorrectas.
- Opción para jugar nuevamente.
- Colores ANSI sin dependencias externas.

## Tecnologías utilizadas

### Lenguajes

- JavaScript (ES Modules)
- JSON
- Markdown

### Frameworks

- No se identificaron frameworks a partir del código fuente.

### Librerías y módulos principales

Todos los módulos utilizados en la aplicación son nativos de Node.js:

- `node:fs/promises`
- `node:path`
- `node:url`
- `node:readline`

### Runtime

- Node.js `>=18.0.0`

### Base de datos

- No se utiliza una base de datos.
- La persistencia del contenido del cuestionario se realiza mediante el archivo `test-app/test-app/data/questions.json`.

### Herramientas

- npm
- Node.js Test Runner (`node --test`)

### Infraestructura

- No se identificaron contenedores, orquestación, infraestructura como código ni configuración de despliegue a partir del repositorio analizado.

## Arquitectura

La arquitectura identificada es una aplicación CLI monolítica y local, dividida en módulos con responsabilidades separadas.

### Componentes principales

- **`test-app/test-app/index.js`**
  - Punto de entrada de la aplicación.
  - Carga el archivo de preguntas.
  - Controla el flujo principal del juego.
  - Maneja selección de categoría, cantidad de preguntas y reinicio.

- **`test-app/test-app/src/quiz.js`**
  - Implementa la clase `Quiz`.
  - Gestiona el estado del juego, el orden de preguntas, la puntuación, el progreso y los resultados.

- **`test-app/test-app/src/input.js`**
  - Encapsula el uso de `readline`.
  - Implementa prompts, selección de opciones, confirmaciones y pausas por Enter.

- **`test-app/test-app/src/colors.js`**
  - Gestiona el formateo visual de la salida por consola usando secuencias ANSI.

- **`test-app/test-app/data/questions.json`**
  - Almacena categorías, preguntas, opciones, índices de respuesta correcta y explicaciones.

### Frontend

- No existe frontend web.
- La interfaz de usuario es exclusivamente por terminal.

### Backend

- No existe backend HTTP ni servicio remoto.
- Toda la lógica se ejecuta localmente dentro del proceso de Node.js.

### APIs

- No se identificaron APIs REST, GraphQL ni endpoints HTTP.

### Persistencia

- Persistencia basada en archivo JSON local.

### Comunicación entre componentes

- Importaciones ES Modules entre archivos JavaScript.
- Entrada y salida estándar (`stdin` / `stdout`) para la interacción con el usuario.

### Flujo general de funcionamiento

```text
Usuario
  ↓
CLI por terminal
  ↓
index.js
  ├─ carga questions.json
  ├─ usa input.js para interacción
  ├─ usa quiz.js para lógica del juego
  └─ usa colors.js para salida formateada
```

## Estructura del proyecto

```text
.
├── README.md                         # Documentación principal del repositorio
└── test-app/
    └── test-app/
        ├── index.js                 # Punto de entrada de la aplicación CLI
        ├── package.json             # Metadatos, scripts y requisito de Node.js
        ├── data/
        │   └── questions.json       # Banco de preguntas y categorías
        └── src/
            ├── colors.js            # Utilidades de color para la terminal
            ├── input.js             # Manejo de entrada interactiva del usuario
            └── quiz.js              # Lógica principal del cuestionario
```

> El código ejecutable del proyecto se encuentra dentro de `test-app/test-app`.

## Requisitos previos

- Node.js `>=18.0.0`
- npm
- Terminal compatible con aplicaciones interactivas de Node.js
- Soporte para salida ANSI si se desea ver colores en consola

## Instalación

1. Clona el repositorio:

```bash
git clone https://github.com/oddiemva/test-app.git
```

2. Accede al directorio de la aplicación:

```bash
cd test-app/test-app
```

3. Instala dependencias:

```bash
npm install
```

### Nota sobre dependencias

A partir de `package.json`, no se identificaron dependencias ni dependencias de desarrollo externas. La aplicación utiliza exclusivamente módulos nativos de Node.js.

## Configuración

### Variables de entorno

- No se encontraron archivos `.env`, `.env.example` ni referencias a variables de entorno en el código fuente.

### Archivos de configuración

- **`test-app/test-app/package.json`**
  - Define el nombre del paquete (`quiz-cli`), versión, scripts, licencia y versión mínima de Node.js.

- **`test-app/test-app/data/questions.json`**
  - Define el contenido del cuestionario.

### Parámetros importantes

No se identificaron flags de línea de comandos ni parámetros externos configurables.

El comportamiento del quiz depende de la estructura de `questions.json`, que contiene:

- `categories`: conjunto de categorías disponibles;
- `name`: nombre visible de la categoría;
- `questions`: lista de preguntas de la categoría;
- `question`: texto de la pregunta;
- `options`: opciones de respuesta;
- `answer`: índice numérico de la opción correcta;
- `explanation`: explicación mostrada tras responder.

## Ejecución

Desde `test-app/test-app`:

```bash
npm start
```

Comando equivalente definido en `package.json`:

```bash
node index.js
```

## Ejemplos de uso

### Flujo esperado en terminal

1. La aplicación muestra un banner de bienvenida.
2. Solicita elegir una categoría.
3. Solicita elegir cuántas preguntas responder.
4. Inicia el cuestionario tras una pausa con Enter.
5. Muestra cada pregunta con opciones numeradas.
6. Indica si la respuesta fue correcta o incorrecta.
7. Muestra una explicación, si existe.
8. Al finalizar, presenta el resultado final y pregunta si se desea volver a jugar.

### Categorías identificadas

A partir de `questions.json`, el proyecto incluye estas categorías:

- JavaScript Basics
- Node.js Fundamentals
- General Programming

### Ejemplo de inicio

```bash
cd test-app/test-app
npm start
```

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

Los scripts definidos en `test-app/test-app/package.json` son:

| Script | Comando | Descripción |
|---|---|---|
| `start` | `node index.js` | Inicia la aplicación de cuestionario en la terminal. |
| `test` | `node --test` | Ejecuta el runner de pruebas nativo de Node.js. |

## Pruebas

Para ejecutar las pruebas definidas por el proyecto:

```bash
npm test
```

### Observaciones

- Existe un script de pruebas configurado.
- No se identificaron archivos de prueba en el repositorio analizado.
- No se pudo determinar a partir del código fuente qué casos de prueba están implementados realmente.

## Despliegue

- No se identificó un proceso formal de despliegue.
- No se encontraron `Dockerfile`, `docker-compose.yml`, workflows de GitHub Actions, archivos de infraestructura ni scripts de publicación.
- El proyecto parece estar orientado a ejecución local como aplicación CLI.

## Datos del cuestionario

El archivo `test-app/test-app/data/questions.json` organiza el contenido en tres categorías:

- **JavaScript Basics**
- **Node.js Fundamentals**
- **General Programming**

Cada pregunta contiene:

- enunciado;
- opciones disponibles;
- índice de respuesta correcta;
- explicación posterior a la respuesta.

Para ampliar el cuestionario, se pueden agregar nuevas categorías o preguntas respetando esta estructura.

## Contribución

No se encontró un archivo `CONTRIBUTING.md`. A partir de la estructura actual del proyecto, un flujo razonable para colaborar sería:

1. Crear una rama para el cambio.
2. Modificar la lógica de la aplicación o el contenido de `questions.json`.
3. Ejecutar la aplicación localmente con `npm start`.
4. Ejecutar `npm test`.
5. Abrir un Pull Request describiendo el cambio realizado.

### Consideraciones para contribuir

- Mantener el formato actual de `questions.json`.
- Conservar la compatibilidad con Node.js `>=18.0.0`.
- Mantener el estilo modular existente en `src/`.

## Licencia

El archivo `package.json` declara licencia **MIT**.

No se encontró un archivo `LICENSE` independiente en el repositorio analizado.

## Autoría

No se pudo determinar la autoría o los mantenedores a partir del código fuente analizado.
