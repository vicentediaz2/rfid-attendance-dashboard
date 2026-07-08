# Dashboard Web - Sistema de Monitoreo Logístico

Este repositorio contiene el dashboard web de un sistema de monitoreo logístico desarrollado como proyecto académico. La aplicación permite visualizar en tiempo real la información generada por el módulo IoT, proporcionando una interfaz centralizada para consultar el estado de las operaciones y los registros de ingreso y salida de camiones.

El sistema está diseñado para trabajar junto con el módulo IoT, encargado de capturar los eventos mediante tarjetas RFID y almacenarlos en Firebase.

> Repositorio del módulo IoT: https://github.com/vicentediaz2/rfid-attendance-dashboard

---

# Arquitectura del sistema

El sistema completo está compuesto por cuatro componentes:

1. **Módulo IoT**

   * ESP32 con lector RFID RC522.
   * Captura el UID de las tarjetas RFID.
   * Envía cada lectura a Firebase Realtime Database.

2. **Base de datos**

   * Firebase Realtime Database.
   * Centraliza los registros generados por el módulo IoT.

3. **Backend**

   * Desarrollado con Express.
   * Consulta la información almacenada.
   * Expone una API REST utilizada por el frontend.

4. **Frontend**

   * Desarrollado con React y Vite.
   * Presenta la información mediante un dashboard orientado al monitoreo de operaciones.

---

# Funcionalidades

El dashboard se organiza en tres vistas principales.

## Dashboard

Vista principal del sistema.

Incluye indicadores y componentes de monitoreo como:

* Estado de los sensores.
* Alertas del sistema.
* Operaciones en curso.
* Indicadores generales.
* Visualizaciones gráficas para facilitar la interpretación de la información.

## Log de camiones

Presenta el historial de movimientos registrados por el sistema.

Cada registro incluye información como:

* Patente del vehículo.
* Último movimiento (entrada o salida).
* Puerta utilizada.
* Fecha y hora del evento.

Los registros son obtenidos desde Firebase y representan los eventos generados por el módulo IoT.

## Camiones en planta

Muestra un resumen de los vehículos que actualmente se encuentran dentro de la planta.

Esta vista se obtiene considerando el último movimiento registrado para cada camión, identificando aquellos cuyo evento más reciente corresponde a una entrada.

---

# Tecnologías utilizadas

## Frontend

* React
* Vite

## Backend

* Node.js
* Express

## Base de datos

* Firebase Realtime Database
* Firebase Admin SDK

---

# Estructura del proyecto

```text
.
├── server/        # Backend y API REST
├── src/           # Aplicación React
├── scripts/       # Scripts de desarrollo y utilidades
├── dist/          # Build de producción
├── package.json
└── index.html
```

---

# API

El backend expone distintos endpoints utilizados por la aplicación.

### Estado del servicio

```text
GET /api/health
```

### Registros

```text
GET /api/logs
GET /api/logs/recent
GET /api/logs/latest-by-sensor
```

### Estado de camiones

```text
GET /api/trucks/state
```

### Eventos de camiones

```text
GET /api/truck-events
POST /api/truck-events
```

---

# Ejecución

Instalar dependencias:

```bash
npm install
```

Iniciar frontend y backend en desarrollo:

```bash
npm run dev:full
```

O ejecutar cada servicio por separado:

Frontend

```bash
npm run dev
```

Backend

```bash
npm run dev:server
```

---

# Firebase

El backend puede utilizar Firebase como sistema de persistencia mediante Firestore.

Para ello es necesario:

* Crear un proyecto en Firebase.
* Configurar las credenciales mediante un Service Account o variables de entorno.
* Configurar el driver correspondiente.

También es posible migrar registros locales a Firebase ejecutando:

```bash
npm run seed:firebase
```

---

# Proyecto relacionado

Este dashboard forma parte de un sistema distribuido de monitoreo logístico basado en RFID.

El firmware encargado de capturar los eventos se encuentra en el siguiente repositorio:

https://github.com/vicentediaz2/rfid-attendance-dashboard