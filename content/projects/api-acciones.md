+++
title = "API de compra y venta de acciones"
date = "2026-10-01"
description = "Backend de microservicios en Spring Boot para operar acciones: cotizaciones en tiempo real, órdenes de compra y venta, y portfolio de cada usuario, con autenticación por Keycloak."
github = "https://github.com/FrancoPrado1144/APIAcciones"
tags = ["java", "spring-boot", "microservicios", "docker", "keycloak"]
categories = ["backend"]
featured = true
+++

Trabajo práctico integrador de Backend de Aplicaciones (UTN FRC, 2026), hecho en grupo. Es el backend de una plataforma para comprar y vender acciones: cada usuario tiene un saldo y un portfolio, consulta cotizaciones y emite órdenes que, al ejecutarse, actualizan sus tenencias.

## Arquitectura

El sistema está dividido en tres microservicios detrás de un API Gateway, cada uno con su responsabilidad:

- **Cotización:** obtiene el precio de cada acción desde la API de Yahoo Finance y lo convierte a pesos con el tipo de cambio del día.
- **Portfolio:** administra el saldo de cada usuario y sus tenencias. Calcula el valor total del portfolio a precios actuales y valida si alcanza el saldo para una operación.
- **Transacción:** gestiona las órdenes de compra y de venta, registra las transacciones y guarda el historial de operaciones. Antes de ejecutar una orden consulta al servicio de portfolio.

![Diagrama de componentes del sistema](/images/projects/api-acciones-componentes.jpg)

## Puntos destacados

- **API Gateway** con Spring Cloud Gateway, que enruta cada grupo de endpoints a su microservicio.
- **Seguridad** con Keycloak y OAuth2: los servicios validan tokens JWT y hay endpoints reservados para administradores.
- **Comunicación entre servicios** por REST, con manejo de errores para cuando otro servicio no responde.
- **Integración con APIs externas** (Yahoo Finance y tipo de cambio), con valores por defecto si el servicio externo falla.
- **Observabilidad** con Loki, Promtail y Grafana para centralizar los logs de todos los servicios.
- **Todo el entorno se levanta con Docker Compose**: los microservicios, el gateway, PostgreSQL, Keycloak y el stack de monitoreo.
- Los endpoints se probaron con colecciones de Postman.

## Tecnologías

Java · Spring Boot · Spring Cloud Gateway · Spring Security · JPA · PostgreSQL · Keycloak · Docker Compose · Grafana / Loki · Postman
