# AEMET API Unofficial

Este proyecto proporciona un cliente TypeScript/JavaScript para interactuar con la API de AEMET (Agencia Estatal de Meteorología) en España. Permite obtener datos meteorológicos, predicciones y valores climatológicos de manera sencilla y eficiente. Este cliente está disponible como un paquete npm llamado `aemet_api_unofficial`.

## Tabla de Contenidos

- [Instalación](#instalación)
- [Uso](#uso)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Ejemplos](#ejemplos)
- [Métodos de la Clase Aemet](#métodos-de-la-clase-aemet)
- [Pruebas](#pruebas)
- [Contribuciones](#contribuciones)
- [Licencia](#licencia)

## Instalación

Para instalar el paquete, puedes usar npm:

```bash
npm install aemet_api_unofficial
```

O si prefieres clonar el repositorio y trabajar directamente con el código fuente:

1. Clona el repositorio:
   ```bash
   git clone https://github.com/tu_usuario/tu_repositorio.git
   cd tu_repositorio
   ```

2. Instala las dependencias:
   ```bash
   npm install
   ```

3. Crea un archivo `.env` en la raíz del proyecto y añade tu clave de API de AEMET:
   ```plaintext
   AEMET_API_KEY=tu_api_key
   ```

## Uso

Para utilizar el cliente de AEMET, primero debes importar la clase `Aemet` y crear una instancia con tu clave de API. Aquí hay un ejemplo básico:

```typescript
import { Aemet } from 'aemet_api_unofficial'; // Cambia la ruta si usas el código fuente
import dotenv from 'dotenv';

dotenv.config();

const apiKey = process.env.AEMET_API_KEY;
const aemet = new Aemet(apiKey);

// Ejemplo de uso
async function obtenerPrediccion() {
    const codigoMunicipio = '28079'; // Código del municipio de Madrid
    const prediccion = await aemet.getSimpleForecast(codigoMunicipio);
    console.log(prediccion);
}

obtenerPrediccion();
```

## Estructura del Proyecto

El proyecto está organizado en varias carpetas y archivos:

- **src/**: Contiene el código fuente del cliente AEMET.
  - **aemet.ts**: Clase principal que maneja la interacción con la API de AEMET.
  - **lib/**: Contiene utilidades, constantes y tipos utilizados en el cliente.
  - **tests/**: Contiene pruebas unitarias para asegurar la funcionalidad del cliente.
  - **examples/**: Ejemplos de uso del cliente para diferentes funcionalidades.
  - **index.ts**: Punto de entrada principal para la librería.

## Ejemplos

El directorio `examples` contiene varios scripts que demuestran cómo utilizar la API de AEMET:

### 1. Obtener Predicción Simplificada

```typescript
import { Aemet } from 'aemet_api_unofficial';
import dotenv from 'dotenv';

dotenv.config();

const aemet = new Aemet(process.env.AEMET_API_KEY);

async function obtenerPrediccionSimplificada() {
    const codigoMunicipio = '28079'; // Madrid
    try {
        const prediccion = await aemet.getSimpleForecast(codigoMunicipio);
        console.log('Predicción Simplificada:', prediccion);
    } catch (error) {
        console.error('Error al obtener la predicción:', error);
    }
}

obtenerPrediccionSimplificada();
```

### 2. Obtener Predicción Completa

```typescript
async function obtenerPrediccionCompleta() {
    const codigoMunicipio = '28079'; // Madrid
    try {
        const prediccionCompleta = await aemet.getForecast(codigoMunicipio);
        console.log('Predicción Completa:', JSON.stringify(prediccionCompleta, null, 2));
    } catch (error) {
        console.error('Error al obtener la predicción completa:', error);
    }
}

obtenerPrediccionCompleta();
```

### 3. Listar Municipios Disponibles

```typescript
async function listarMunicipios() {
    try {
        const municipios = await aemet.getMunicipalities();
        console.log('Municipios Disponibles:', municipios);
    } catch (error) {
        console.error('Error al listar municipios:', error);
    }
}

listarMunicipios();
```

### 4. Obtener Alertas Meteorológicas

```typescript
async function obtenerAlertasHoy() {
    try {
        const alertas = await aemet.getAlertsToday();
        console.log('Alertas Meteorológicas de Hoy:', alertas);
    } catch (error) {
        console.error('Error al obtener alertas:', error);
    }
}

obtenerAlertasHoy();
```

## Métodos de la Clase Aemet

La clase `Aemet` incluye varios métodos útiles para interactuar con la API de AEMET:

- **getSimpleForecast(municipalityCode: string)**: Obtiene la predicción simplificada para un municipio dado su código INE (5 dígitos). Devuelve un objeto con la predicción para hoy, mañana y pasado mañana.

- **getForecast(municipalityCode: string)**: Obtiene la predicción completa para un municipio, incluyendo datos crudos.

- **getMunicipalities()**: Devuelve una lista de municipios disponibles con sus códigos.

- **getProvinces()**: Devuelve una lista de provincias disponibles.

- **getAlertsToday()**: Obtiene los avisos meteorológicos para el día actual.

- **getAlertsTomorrow()**: Obtiene los avisos meteorológicos para el día siguiente.

- **getWeatherStations()**: Devuelve una lista de estaciones meteorológicas disponibles.

- **searchWeatherStations(query: string)**: Busca estaciones por nombre o provincia.

- **getClimateValues(params: ClimateValuesParams)**: Obtiene valores climatológicos diarios para una estación y período específicos.

- **getClimateSummaryByProvincia(params: ClimateValuesParams, provincia: string)**: Obtiene un resumen climatológico para una estación y período, filtrando por provincia.

## Pruebas

Para ejecutar las pruebas, utiliza los siguientes comandos:

```bash
# Ejecutar todos los tests
npm test

# Ejecutar tests en modo watch
npm run test:watch

# Ejecutar tests con informe de cobertura
npm run test:coverage
```

Las pruebas están organizadas en el directorio `tests` y utilizan Jest para la ejecución de pruebas.

## Contribuciones

Las contribuciones son bienvenidas. Si deseas contribuir, por favor sigue estos pasos:

1. Haz un fork del repositorio.
2. Crea una nueva rama (`git checkout -b feature/nueva-caracteristica`).
3. Realiza tus cambios y haz commit (`git commit -m 'Añadir nueva característica'`).
4. Haz push a la rama (`git push origin feature/nueva-caracteristica`).
5. Abre un Pull Request.

## Licencia

Este proyecto está bajo la Licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.