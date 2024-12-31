# Interbanking Challenge

## Descripción
Este proyecto implementa una API utilizando **NestJS** con arquitectura **hexagonal**, diseñada para exponer tres endpoints que cumplen con los siguientes requerimientos:

- Listar las empresas que realizaron transferencias durante el último mes.
- Listar las empresas que se adhirieron durante el último mes.
- Registrar la adhesión de una nueva empresa.

Adicionalmente, se incluye un módulo para la gestión de usuarios y la seguridad de la aplicación.

---

## Arquitectura
El proyecto utiliza una arquitectura **hexagonal (Ports and Adapters)** para garantizar un diseño flexible, desacoplado y fácilmente mantenible. La API está compuesta por los siguientes módulos:

### **Módulos**

#### 1. Companies
Responsable de exponer los tres endpoints principales que cumplen con los requerimientos del challenge. Este módulo maneja:

- La obtención de empresas basándose en criterios temporales.
- La gestión de adhesiones.
- Se agregaron transferencias por default en la migracion del esquema company (conciderando que no es parte del requerimiento el endpoint para dar de alta transferencias).

#### 2. User
Encargado de gestionar la seguridad de la aplicación, incluyendo:

- Autenticación de usuarios (Login).
- Creación y actualización de usuarios.

---

## Capas de la Arquitectura Hexagonal
Cada módulo está diseñado siguiendo las tres capas principales de la arquitectura hexagonal:

### 1. **Domain**
Esta capa contiene la lógica de negocio central y está desacoplada de cualquier detalle técnico. Incluye:

- **Entidades:** Definición de las estructuras principales del dominio (por ejemplo, `Company`, `User`).
- **Puertos:** Interfaces que definen los contratos para:
  - Puertos de entrada: Llamados desde la capa de aplicación (por ejemplo, casos de uso).
  - Puertos de salida: Implementados por adaptadores en la capa de infraestructura (por ejemplo, repositorios).

### 2. **Application**
La capa de aplicación actúa como el intermediario entre la lógica de negocio y la infraestructura. Incluye:

- **Casos de uso:** Coordinan la lógica de negocio y la implementación de los adaptadores. Ejemplos:

### 3. **Infrastructure**
Esta capa implementa los detalles técnicos, como:

- **Adaptadores de entrada:** Los controladores HTTP que reciben las solicitudes y llaman a los casos de uso correspondientes.
- **Adaptadores de salida:** Implementaciones concretas de los puertos de salida, como repositorios que interactúan con bases de datos (userRepository y companyRepository)
- **Configuraciones:** Configuraciones para el servidor HTTP, Prisma, y otros servicios.

## Tecnologías Utilizadas
- **NestJS**: Framework principal para el desarrollo de la API.
- **Prisma**: ORM para la gestión de la base de datos.
- **TypeScript**: Lenguaje principal para el desarrollo.
- **Jest**: Framework para pruebas unitarias

---

## Instalación y Ejecución

### Requisitos Previos
- Node.js (v18 o superior)
- Base de datos (postgresql configurada con Prisma)

### Pasos

1. Clona el repositorio:

   ```bash
   git clone https://github.com/tu-usuario/interbanking-challenge.git](https://github.com/hlovey84/interbanking-chanllenge.git
   cd interbanking-challenge
   ```

2. Generamos los contenedores de docker. Desde la carpeta raiz del proyecto:
    ```bash
   docker-compose build
   docker-compose up -d
   ```
3. ir a la documentacion de swagger
   
   http://localhost:3000/api#/

---

## Endpoints

### **1. Obtener Empresas con Transferencias**
- **Método:** GET
- **URL:** `/companies/transfers`
- **Descripción:** Devuelve una lista de empresas que realizaron transferencias en el último mes.

### **2. Obtener Empresas Adheridas**
- **Método:** GET
- **URL:** `/companies/new`
- **Descripción:** Devuelve una lista de empresas que se adhirieron en el último mes.

### **3. Registrar una Nueva Empresa**
- **Método:** POST
- **URL:** `/companies`
- **Body:**

   ```json
   {
     "cuit": "12345678901",
     "razonSocial": "Empresa Ejemplo",
     "fechaAdhesion": "2024-12-01"
   }
   ```
- **Descripción:** Registra la adhesión de una nueva empresa.

---

## Pruebas
Ejecuta las pruebas con el siguiente comando:

```bash
pnpm run test
```

