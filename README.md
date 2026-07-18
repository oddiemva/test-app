# Quiz CLI

Aplicación de línea de comandos escrita en Node.js para ejecutar cuestionarios interactivos de programación. El proyecto carga preguntas desde un archivo JSON, permite elegir una categoría, seleccionar la cantidad de preguntas y muestra un resumen final con puntuación y revisión de errores.

## Descripción general

Este proyecto implementa un juego tipo quiz ejecutado en terminal. Su propósito es ofrecer una forma simple e interactiva de practicar conocimientos de programación, especialmente sobre:

- JavaScript
- Node.js
- Programación general

La aplicación:

- muestra un menú de categorías,
- permite elegir cuántas preguntas responder,
- presenta preguntas de opción múltiple,
- valida las respuestas,
- muestra explicaciones,
- calcula la puntuación final,
- y permite volver a jugar.

## Características

- Interfaz interactiva por terminal.
- Selección de categoría de preguntas.
- Selección de cantidad de preguntas:
  - todas,
  - 3 preguntas,
  - 5 preguntas.
- Preguntas de opción múltiple.
- Barajado de preguntas.
- Barra de progreso durante la partida.
- Resultado final con porcentaje.
- Mensaje de desempeño según la puntuación.
- Revisión de preguntas incorrectas.
- Salida coloreada usando códigos ANSI.
- Implementación modular con ES Modules.

## Tecnologías utilizadas

### Lenguajes

- JavaScript

### Runtime

- Node.js `>=18.0.0`

### Frameworks

- No se identificaron frameworks externos a partir del código fuente.

### Librerías y módulos

#### Módulos nativos de Node.js

- `node:fs/promises`
- `node:url`
- `node:path`
- `node:readline`

#### Dependencias externas

- No se encontraron dependencias externas en `package.json`.

### Formato de datos

- JSON para almacenamiento de preguntas (`data/questions.json`)

### Herramientas

- npm, a través de los scripts definidos en `package.json`

## Arquitectura

La aplicación sigue una arquitectura simple y modular orientada a CLI:

- **`index.js`**: punto de entrada de la aplicación.
- **`src/input.js`**: manejo de entrada del usuario mediante `readline`.
- **`src/quiz.js`**: lógica principal del juego, puntuación y resultados.
- **`src/colors.js`**: utilidades para formateo de texto con colores ANSI.
- **`data/questions.json`**: fuente de datos de preguntas y categorías.

### Flujo general

1. La aplicación inicia en `index.js`.
2. Se cargan las preguntas desde `data/questions.json`.
3. El usuario elige una categoría.
4. El usuario elige cuántas preguntas responder.
5. Se crea una instancia de `Quiz`.
6. Las preguntas se presentan una a una.
7. Se valida cada respuesta y se almacena el resultado.
8. Al finalizar, se muestra un resumen con:
   - puntuación,
   - porcentaje,
   - mensaje de rendimiento,
   - revisión de respuestas incorrectas.
9. El usuario puede decidir si desea volver a jugar.

### Componentes identificados

- **Frontend**: no aplica; es una aplicación CLI.
- **Backend**: no aplica como servicio web.
- **API**: no se identificaron APIs HTTP o servicios externos.
- **Persistencia**: archivo local JSON.
- **Base de datos**: no se identificó ninguna base de datos.
- **Puertos**: no aplica; la aplicación no expone servicios de red.

## Estructura del proyecto

```text
.
├── README.md
└── test-app/
    └── test-app/
        ├── index.js                # Punto de entrada de la aplicación CLI
        ├── package.json            # Metadatos, scripts y requisito de Node.js
        ├── data/
        │   └── questions.json      # Banco de preguntas por categoría
        └── src/
            ├── colors.js           # Utilidades de color para la terminal
            ├── input.js            # Captura y validación de entradas del usuario
            └── quiz.js             # Lógica del quiz, progreso y resultados
```

## Requisitos previos

- Node.js `>=18.0.0`
- npm

## Instalación

No se encontraron dependencias externas declaradas en `package.json`, por lo que el proyecto depende únicamente de Node.js y de módulos nativos.

### 1. Clonar el repositorio

```bash
git clone https://github.com/oddiemva/test-app.git
```

### 2. Entrar al directorio de la aplicación

El código ejecutable se encuentra dentro de un subdirectorio:

```bash
cd test-app/test-app
```

### 3. Verificar la versión de Node.js

```bash
node --version
```

Debe ser compatible con `>=18.0.0`.

## Configuración

### Variables de entorno

No se encontraron archivos `.env`, `.env.example` ni referencias a variables de entorno en el código fuente analizado.

### Archivos de configuración relevantes

- `test-app/test-app/package.json`
- `test-app/test-app/data/questions.json`

### Parámetros importantes

El contenido del cuestionario depende de `data/questions.json`, cuya estructura incluye:

- categorías,
- nombre de categoría,
- preguntas,
- opciones,
- índice de respuesta correcta,
- explicación.

## Ejecución

Desde `test-app/test-app`:

### Usando npm

```bash
npm start
```

### Usando Node.js directamente

```bash
node index.js
```

## Ejemplos de uso

Al iniciar, la aplicación muestra un banner y solicita elegir una categoría:

```text
Choose a category:

  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming
```

Luego solicita cuántas preguntas responder:

```text
How many questions?

  1. All questions
  2. 3 questions
  3. 5 questions
```

Durante el juego, el usuario responde ingresando el número de la opción:

```text
Your choice (enter number):
```

Al finalizar, se muestra un resumen con:

- categoría,
- puntuación total,
- porcentaje,
- mensaje de desempeño,
- repaso de preguntas incorrectas.

## Scripts disponibles

Definidos en `test-app/test-app/package.json`:

| Script | Comando | Descripción |
|---|---|---|
| `start` | `node index.js` | Inicia la aplicación CLI. |
| `test` | `node --test` | Ejecuta las pruebas usando el runner nativo de Node.js. |

## Pruebas

El repositorio define el script:

```bash
npm test
```

Sin embargo, en la estructura analizada no se encontraron archivos de prueba. Por lo tanto, no se pudo determinar a partir del código fuente si actualmente existen pruebas implementadas para ejecutar.

## Contenido funcional identificado

### Categorías incluidas

Según `data/questions.json`, el proyecto incluye:

- **JavaScript Basics**
- **Node.js Fundamentals**
- **General Programming**

### Comportamientos implementados

- Carga de preguntas desde archivo local.
- Selección validada de opciones.
- Confirmación para volver a jugar.
- Cálculo de progreso en porcentaje.
- Barajado de preguntas con algoritmo Fisher-Yates.
- Resumen de respuestas incorrectas para repaso.

## Despliegue

No se encontraron archivos o configuraciones de despliegue como:

- `Dockerfile`
- `docker-compose.yml`
- workflows de GitHub Actions
- archivos de infraestructura
- configuraciones de hosting

No se pudo determinar a partir del código fuente un proceso formal de despliegue. Por la naturaleza del proyecto, se trata de una aplicación local de terminal.

## Contribución

No se encontraron guías específicas de contribución en el repositorio analizado.

Si deseas colaborar, una contribución razonable sería:

1. crear una rama,
2. realizar cambios,
3. validar la ejecución del proyecto,
4. abrir un Pull Request.

## Licencia

El archivo `package.json` indica licencia:

- **MIT**

## Autoría

No se pudo determinar a partir del código fuente información explícita sobre autores o mantenedores.
