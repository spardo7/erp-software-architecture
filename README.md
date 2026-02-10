# ERP Empresarial

## Descripción
Este proyecto es un **Sistema ERP (Enterprise Resource Planning)** que centraliza y automatiza los procesos empresariales de una organización.  
Permite gestionar compras, facturación, stock y costos, activos fijos, empleados y reportes estratégicos (EIS).

El ERP está diseñado como un **monolito con arquitectura de contenedores** para simplificar la integración y el despliegue, con un frontend SPA en React y un backend en Java con Spring Boot, usando PostgreSQL como base de datos.

---

## Módulos Principales

| Módulo             | Funcionalidad principal |
|--------------------|------------------------|
| Compras            | Registrar órdenes de compra, gestionar proveedores y productos |
| Facturación        | Emitir facturas y notas, controlar pagos |
| Stock/Costos       | Control de inventario, costos y movimientos de productos |
| Activos Fijos      | Registro y depreciación de activos de la empresa |
| Empleados          | Gestión de información y roles de empleados |
| EIS                | Reportes, KPIs y análisis estratégico para la toma de decisiones |

---

## Historia de Usuario Ejemplo

**Como gestor de inventario, quiero registrar nuevos productos para poder mantener actualizado el stock y las órdenes de compra.**

Este escenario crítico está documentado en la **Vista de Ejecución (arc42)** con un diagrama de secuencia que describe cómo interactúan SPA, API y base de datos.

---

## Documentación

Toda la documentación del proyecto se encuentra en la carpeta `docs/arc42/`:

- `01_introduction_and_goals.md` – Introducción y metas del ERP.  
- `02_architecture_constraints.md` – Restricciones y decisiones tecnológicas.  
- `03_system_scope_and_context.md` – Diagrama de contexto (C1) y explicación.  
- `05_building_block_view.md` – Diagrama de contenedores (C2) y responsabilidades.  
- `06_runtime_view.md` – Escenarios críticos y diagramas de secuencia.  
- `10_glossary.md` – Glosario de términos clave del ERP.

---

## Requisitos Técnicos

- **Backend:** Java + Spring Boot  
- **Frontend:** React (SPA)  
- **Base de Datos:** PostgreSQL  
- **Despliegue:** Docker (opcional)  

---

## Cómo ejecutar el proyecto

1. Clonar el repositorio:
```bash
git clone <URL_DEL_REPOSITORIO>
