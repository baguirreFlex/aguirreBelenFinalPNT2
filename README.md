# Final PNT2 proyecto Vue

## Conversor de Pesos a Dólares

Aplicación frontend desarrollada con Vue CLI 3 que permite convertir valores en pesos argentinos a dólares estadounidenses.

### Características

- **Conversión Reactiva**: La conversión se realiza automáticamente al cambiar el monto o la cotización
- **Actualización Automática**: Opción para actualizar la cotización del dólar cada 2 segundos desde la API de Bluelytics
- **Modo Manual**: Posibilidad de ingresar la cotización manualmente cuando la actualización automática está deshabilitada

### Instalación

```bash
npm install
```

### Ejecutar en desarrollo

```bash
npm start
```

La aplicación estará disponible en `http://localhost:8080`


### Tecnologías Utilizadas

- Vue 3 
- Bootstrap 5
- Axios
- Vue CLI 3

### Funcionalidades Implementadas

#### Punto 1: Conversión Básica
- Campo de entrada para monto en pesos
- Campo de entrada para cotización del dólar (manual)
- Visualización del resultado convertido en tiempo real

#### Punto 2: Actualización Automática
- Consulta a la API de Bluelytics cada 2 segundos
- Uso del campo `value_sell` del dólar oficial
- Actualización automática del campo de cotización y recálculo

#### Punto 3: Control de Actualización
- Checkbox para habilitar/deshabilitar actualización automática
- Deshabilitación del campo manual cuando está activa la actualización automática
- Visualización de fecha y hora de la última actualización
- Estado inicial: actualización automática deshabilitada
