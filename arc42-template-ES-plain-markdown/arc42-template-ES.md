---
date: Febrero 2026
title: Proyecto ERP - Grupo X
---

# Introducción y Metas {#section-introduction-and-goals}

## Vista de Requerimientos {#_vista_de_requerimientos}

El ERP centraliza y automatiza procesos empresariales: Compras, Facturación, Stock/Costos, Activos Fijos, Empleados y EIS.  
Requisitos principales (Módulo de Compras):

- Registrar nuevas órdenes de compra.  
- Gestionar proveedores y productos asociados.  
- Aprobar o rechazar órdenes de compra.  
- Consultar órdenes de compra y su historial.  
- Integración con Stock y Facturación para reflejar inventario y costos.

## Metas de Calidad {#_metas_de_calidad}

- Sistema confiable y disponible 24/7 para usuarios internos.  
- Respuesta rápida en la SPA (< 2s por operación crítica).  
- Integridad de datos entre Compras, Stock y Facturación.

## Partes interesadas (Stakeholders) {#_partes_interesadas_stakeholders}

+-------------+---------------------------+---------------------------+
| Rol/Nombre  | Contacto                  | Expectativas              |
+=============+===========================+===========================+
| Gestor de Compras | gestor@empresa.com     | Registro y control eficiente de compras |
+-------------+---------------------------+---------------------------+
| Administrador ERP | admin@empresa.com      | Supervisión y reportes centralizados |
+-------------+---------------------------+---------------------------+
| Empleado | empleado@empresa.com        | Acceso a información de stock y facturas |
+-------------+---------------------------+---------------------------+

# Restricciones de la Arquitectura {#section-architecture-constraints}

- Backend: Java con Spring Boot (monolito).  
- Frontend: SPA con React.  
- Base de datos: PostgreSQL.  
- API RESTful para comunicación entre frontend y backend.  
- Contenedores opcionales con Docker para despliegue.  

# Alcance y Contexto del Sistema {#section-context-and-scope}

## Contexto de Negocio {#_contexto_de_negocio}

El ERP permite a usuarios internos (administradores y empleados) gestionar compras, stock, facturación, activos fijos, empleados y KPIs consolidados. Se conecta con proveedores y servicios externos de facturación.

## Contexto Técnico {#_contexto_técnico}

El sistema consiste en un frontend SPA, una API monolítica y una base de datos central.  
![Diagrama de Contexto](./images/c1_context.png)

# Estrategia de solución {#section-solution-strategy}

Se utiliza un enfoque monolítico inicial para simplificar la integración de módulos, con posibilidad de modularización futura. La arquitectura está basada en contenedores (SPA, API, DB).

# Vista de Bloques {#section-building-block-view}

## Sistema General de Caja Blanca {#_sistema_general_de_caja_blanca}

### Aplicación Web (SPA) {#_caja_negra_spa}

Interfaz de usuario para administradores y empleados.  
Responsable de:  
- Registrar productos y órdenes de compra.  
- Consultar stock, facturación y reportes.  

Interfase: API RESTful con backend.

### API Monolítica {#_caja_negra_api}

Lógica de negocio del ERP:  
- Procesa compras, stock, facturación y activos.  
- Valida datos de entrada.  
- Genera reportes consolidados.  

Interfase: REST API para SPA, JDBC para DB.

### Base de Datos ERP {#_caja_negra_db}

Almacena todas las entidades: Productos, Proveedores, Órdenes, Empleados, Activos, Facturación, Stock, KPIs.  

Interfase: SQL con API Monolítica.  

## Nivel 2 - Contenedores {#_nivel_2}

![Diagrama de Contenedores](./images/c2_containers.png)

- **SPA**: Interfaz web para usuarios.  
- **API Monolítica**: Lógica de negocio y reglas.  
- **Base de Datos**: Almacenamiento de datos persistente.  

# Vista de Ejecución {#section-runtime-view}

## Escenario: Registrar un Producto {#_escenario_de_registro_producto}

Flujo:

1. Gestor rellena formulario en SPA.  
2. SPA envía POST /api/productos con datos.  
3. API valida y guarda en DB.  
4. API retorna ID del producto creado.  
5. SPA muestra mensaje de éxito y actualiza lista.

![Diagrama de Secuencia](./images/sequence_register_product.png)

# Vista de Despliegue {#section-deployment-view}

- Servidor Linux con Docker.  
- Contenedores desplegados: SPA (Nginx), API Monolítica, PostgreSQL.  
- Comunicación interna vía red Docker.  
- Backup diario y monitoreo de logs.  

# Conceptos Transversales (Cross-cutting) {#section-concepts}

## Seguridad

- HTTPS obligatorio.  
- Autenticación y autorización por roles.  

## Logs y Monitoreo

- Registro de eventos críticos en API.  
- Monitoreo de disponibilidad y rendimiento.  

# Decisiones de Diseño {#section-design-decisions}

- Arquitectura monolítica inicial para facilitar integración.  
- SPA para mejorar experiencia de usuario.  
- PostgreSQL por su soporte transaccional y consistencia de datos.  

# Requerimientos de Calidad {#section-quality-scenarios}

- Disponibilidad 24/7  
- Tiempo de respuesta < 2s  
- Integridad de datos entre módulos  

# Riesgos y deuda técnica {#section-technical-risks}

- Posible escalabilidad limitada si el ERP crece mucho (monolito).  
- Dependencia de PostgreSQL; migración futura requeriría refactor.  

# Glosario {#section-glossary}

+----------------------+-----------------------------------------------+
| Término              | Definición                                    |
+======================+===============================================+
| Producto             | Artículo disponible para compra y venta.     |
+----------------------+-----------------------------------------------+
| Proveedor            | Entidad que suministra productos.            |
+----------------------+-----------------------------------------------+
| Orden de Compra      | Solicitud de adquisición de productos.       |
+----------------------+-----------------------------------------------+
| Detalle de Orden     | Línea específica de una orden.               |
+----------------------+-----------------------------------------------+
| Empleado             | Persona registrada en el ERP.                |
+----------------------+-----------------------------------------------+
| Activo Fijo          | Bien material o intangible de la empresa.   |
+----------------------+-----------------------------------------------+
| EIS                  | Módulo de reportes y KPIs estratégicos.     |
+----------------------+-----------------------------------------------+
