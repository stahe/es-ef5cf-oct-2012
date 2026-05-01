# Introducción práctica a Entity Framework 5 Code First (octubre de 2012)

Este documento describe una **arquitectura de aplicación ASP.NET flexible y escalable**
y muestra cómo sustituir el ORM **NHibernate** por **Entity Framework 5**
sin modificar la capa de aplicación.

🌐 Se puede acceder al sitio web asociado en: https://stahe.github.io/es-ef5cf-oct-2012/

---

## Antecedentes

**Entity Framework** es un ORM (mapeador relacional de objetos) creado originalmente por Microsoft
y convertido en código abierto en julio de 2012.

En un curso de ASP.NET, este documento se basa en una arquitectura por capas
que permite actualizar tecnologías (ORM, DBMS) sin afectar a la aplicación.

---

## Arquitectura general

El siguiente diagrama muestra las arquitecturas utilizadas en la aplicación:
![Arquitectura ASP.NET con NHibernate y Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D200000183315F4E40.png)

![Arquitectura ASP.NET con Entity Framework 5 y Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D7000001825B1CF7DD.png)

### Descripción de las capas

- **Aplicación ASP.NET**  
  Capa de presentación y lógica de negocio.

- **DAO (Objetos de acceso a datos)**  
  Interfaz de acceso a datos utilizada por la aplicación.

- **ORM (NHibernate / Entity Framework)**  
  Responsable de generar SQL y comunicarse con ADO.NET.

- **ADO.NET**  
  Conector al SGBD.

- **SGBD**  
  Sistema de gestión de bases de datos.

- **Spring.NET**  
  Garantiza la integración de capas y la inyección de dependencias.

---

## ¿Por qué utilizar un ORM?

Vincular la capa DAO directamente a ADO.NET hace que la aplicación dependa del SGBD:

- diferencias en los tipos de datos;
- SQL propietario;
- bibliotecas específicas del SGBD.

Con un ORM, cambiar el SGBD equivale esencialmente a **cambiar la configuración**
del ORM. La capa DAO permanece inalterada.

---

## Función de Spring.NET

Spring.NET permite:

- que la aplicación ASP.NET obtenga una referencia a la capa DAO;
- la creación de esta capa a partir de un archivo de configuración;
- la sustitución de una implementación DAO por otra **sin modificar el código**,
  siempre que la interfaz siga siendo la misma.

---

## Objetivo de este documento

Demostrar en la práctica que la arquitectura:

- es **resistente a los cambios en el SGBD**;
- es **resistente a los cambios en el ORM**;
- permite **sustituir NHibernate por Entity Framework 5**
  sin modificar la capa de aplicación ASP.NET.

---

## Enfoque seguido

La migración se lleva a cabo en varias etapas:

1. Exploración de **Entity Framework 5** con varios SGBD;
2. Creación de una nueva capa de acceso a datos (**DAO2**);
3. Conexión de la aplicación ASP.NET existente a esta nueva capa DAO.

---

## Destinatarios

- Desarrolladores de ASP.NET
- Estudiantes y profesores de arquitectura de software
- Cualquier persona interesada en arquitecturas desacopladas y escalables

---

## Licencia y uso

Documento educativo destinado a la enseñanza y demostración
de arquitecturas de aplicaciones escalables.

Serge Tahé, Octubre de 2012