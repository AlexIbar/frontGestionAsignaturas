
![Logo](https://www.redttu.edu.co/es/wp-content/uploads/2019/03/11.-IU-DIGITAL.png)

## EA3: Evidencia de Aprendizaje 4: Reto final
## Gestion de Asignaturas

Front que hace consumo de la API desarrollada en PHP entregadas en conjunto para la entrega del trabajo final
Enlace: back -> https://github.com/AlexIbar/backGestionAsignaturas

## Authors

- [@AlexIbar](https://github.com/AlexIbar)
Edwin Alexander Ibarra Ortiz - PREELEC2202PC-TDS0033 
- [@chechorios2008](https://github.com/chechorios2008)
Sergio Andres Rios Gomez - PREELEC2202PC-TDS0033


## Repositorio GitHub
[![portfolio](https://pythonforundergradengineers.com/posts/git/images/git_and_github_logo.png)](https://github.com/)
Enlace: https://github.com/AlexIbar/frontGestionAsignaturas

# Descripción del front

### General
El sistema nos permite realizar la gestion de asignaturas, roles y usuarios. el sistema de administra de acuerdo al rol del usuario, teniendo en cuenta las necesidades planteadas en el archivo soporte del proyecto

### Comandos para iniciar el proyecto

## Installation


```bash
  npm install
  npm run dev #Para desarrollo
  npm run build #Compilar a producción
```

Tener en cuenta que para que el front pueda funcionar el proyecto del back debe de estar corriendo y se debe actualizar

## Se debe tener previamente

```sql
  insert into rols(id, nombre) VALUES (1, 'COORD')
  insert into rols(nombre) VALUES ('EST')
  insert into rols(nombre) VALUES ('PROF')
```
El rol ADMIN -> Es el que se encargara de crear los usuarios y roles asociados a los usuarios

```sql
   insert into usuarios(nombre, correo, password, id_rol) VALUES('Administrador', 'sergio.rios@gmail.com','$2y$12$FUq30sLT.dylLS4VJn8hCOL9Wp7m1aOAcOorIYxiRQsw5sIz4XtCK', 1)
    -- La contraseña es: sergio.rios@gmail.com
```

