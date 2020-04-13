# MySQL SHOW STATEMENT  Pseudo-GUI
### Cheatsheet con comandos para simular una interfaz "grafica"e inspeccionar elementos, estados y ajustes.
Link: ["MySQL Reference Manual SHOW STATEMENTS"](https://dev.mysql.com/doc/refman/8.0/en/show.html "manual")


## Índice
- Inspección de bases, tablas y columnas
    - [DATABASES](#show-DATABASES)
    - [TABLES](#show-TABLES)
    - [COLUMNS](#show-COLUMNS)
- Inspección de codificación y caracteres especiales
    - [CHARACTER SET](#show-CHARACTER-SET)
    - [COLLATION](#show-COLLATION)
- Inspección de permisos y privilegios
    - [PRIVILEGES](#show-PRIVILEGES)
    - [GRANTS](#show-GRANTS)
- Inspección del estado general del servidor
    - [STATUS](#show-STATUS)
    - [PROFILE](#show-PROFILE)
    - [INDEX](#show-INDEX)
    - [LOGS](#show-BINARY-LOGS)
- Inspección de avisos y errores
    - [WARNINGS](#show-WARNINGS)
    - [ERRORS](#show-ERRORS)
- Inspección de eventos, triggers y plugins
    - [PLUGINS](#show-PLUGINS)
    - [TRIGGERS](#show-TRIGGERS)
    - [EVENTS](#show-EVENTS)

#### SHOW DATABASES
Comando para listar las bases de datos o esquemas existentes.
La sintaxis tambien acepta patrones LIKE y expresiones WHERE para una búsqueda mas avanzada.

```sql
SHOW {DATABASES | SCHEMAS}
    [LIKE | WHERE];
```

![scr1](/img2/databases.png)


#### SHOW TABLES 
Comando usado para listar las tablas de una base de datos.
Igual que en caso anterior disponemos de LIKE y WHERE en caso de búsquedas precisas.
```sql
SHOW  TABLES
    [FROM <nombre_BD>]
    [LIKE | WHERE];
```

![scr1](/img2/.png)

#### SHOW COLUMNS
Comando que muestra la informacion sobre columnas en una tabla dada. 
El parametro EXTENDED incluira la información de columnas invisibles, aquellas que MySQL utiliza internamente para su correcto funcionamiento.
```sql
SHOW [EXTENDED | FULL] COLUMNS
    FROM <nombre_tabla>
    [LIKE | WHERE];
```
Los campos mostrados son:
| Columna    | Valores                                                                                        |
|------------|------------------------------------------------------------------------------------------------|
| Field      | nombre del atributo/columna de la tabla                                                        |
| Type       | el DATATYPE del atributo                                                                       |
| Collation  | conjunto de reglas para tratar/comparar strings                                                       |
| Null       | "nulobilidad", valor "YES" permite almacenar NULL                                              |
| Key        | define si la columna esta indexada                                                             |
| Default    | valor por defecto de la columna                                                                |
| Extra      | información adicional como "auto_increment y otros                                             |
| Privileges | privilegios que tiene el usuario actual sobre la columna solo se muestra usando parámetro FULL |
| Comment    | muestra comentarios existentes requiere FULL                                                   |

SHOW COLUMNS es semejante a DESCRIBE COLUMNS:

```sql
DESCRIBE COLUMNS
    FROM <nombre_tabla>;
```

![scr1](/img2/.png)



#### SHOW CHARACTER SET
Lista los encodings soportados (conjunto de caracteres).
Muestra nombre de charset, descripción breve, collation por defecto, maximo número de bytes para almacenar un caracter.
```sql
SHOW CHARACTER SET
    [LIKE | WHERE];
```
![scr1](/img2/.png)

#### SHOW COLLATION
Comando que lista los collation (coonjunto de reglas para tratar caracteres  UNICODE y non-UNICODE).
Por defecto el servidor incluye todos collation-s disponibles.
Muestra nombre, charset asociado, id, si está habilitado por defecto, si esta compilado en el servidor, tamaño de memoria relativo para almacenaje de strings.
```sql
SHOW COLLATION
    [LIKE | WHERE];
```
![scr1](/img2/.png)



#### SHOW PRIVILEGES
Comando que muestra la lista de los privilegios soportados por el servidor
```sql
SHOW PRIVILEGES;
```

![scr1](/img2/.png)

#### SHOW GRANTS
Comando que muestra los privilegios asignados a un usuario concreto.
```sql
SHOW GRANTS
    [FOR <usuario>];
```

![scr1](/img2/.png)


#### SHOW STATUS
Comando que visualiza el estado  del servidor. No requiere privilegios algunos para ser ejecutado.
GLOBAL/SESSION permite elegir si mostrar el estado general o de la sesion actual.
```sql
SHOW [GLOBAL | SESSION] STATUS
    [LIKE | WHERE];
```
![scr1](/img2/.png)

#### SHOW PROFILE
Comando que muestra muestra el consumo de recursos para el comando ejecutado durante la sesión actual.
Podemos especificar que tipo de recurso deseamos monitorizar(type), que comandos trackear, limitar la cantidad de resultados.
```sql
SHOW PROFILE [type [, type] ... ]
    [FOR QUERY n]
    [LIMIT row_count [offset]];

type: {
    ALL
  | BLOCK IO
  | CONTEXT SWITCHES
  | CPU
  | IPC
  | MEMORY
  | PAGE FAULTS
  | SOURCE
  | SWAPS
}
```
![scr1](/img2/.png)


#### SHOW INDEX
Comando que muestra la indexación de una tabla. La indexación es una estructura de datos que mejora el rendimiento de la base de datos.
El comando es útil para trabajar sobre la optimización de velocidades de operaciones. 
Como algunos otros STATEMENTS tambien dota de predicado.
```sql
SHOW [EXTENDED] INDEX
    FROM <nombre_tabla>
    [WHERE];
```

![scr1](/img2/.png)



#### SHOW BINARY LOGS
Comando que muestra los logs de la base de datos. Un log es una lista en la cual están almacenados todos los cambios efectuados a la BD.
Pueden ser replicados, purificados(borrados) etc. Son esenciales para backups.
El comando muestra los logs existentes, su tamaño y si estan encriptados.
```sql
SHOW BINARY LOGS;
```

![scr1](/img2/.png)



#### SHOW WARNINGS
Comando utilizado para diagnóstico del sistema que muestra los avisos del sistema existentes. 
```sql
SHOW WARNINGS [COUNT(*)];
```

![scr1](/img2/.png)


#### SHOW ERRORS
Comando que lista los errores ocurridos, herramienta de diagnóstico.
Permite limitar los resultados o, simplemente, contar sus ocurrencias.
```sql
SHOW ERRORS [LIMIT [offset,] row_count];

SHOW COUNT(*) ERRORS;
```
![scr1](/img2/.png)


#### SHOW PLUGINS 
Comando que lista los plugins existentes en el servidor, su nombre, estado, tipo, libreria (Library) y licencia.
```sql
SHOW PLUGINS;
```

![scr1](/img2/.png)



#### SHOW TRIGGERS
Comando que lista los triggers (disparadores?) establecidos. Muestra Nombre, evento asociado, tabla referente, comandos a ejecutar, temporizador y otros.
```sql
SHOW TRIGGERS
    [LIKE | WHERE];
```

![scr1](/img2/.png)



#### SHOW EVENTS
Comando que muestra los eventos ocurridos, requiere privilegio EVENT para ser ejecutado.
Muestra nombre de BD, nombre del evento, cuenta causante del evento, zona horaria, tipo de evento, sus valores y estados.
```sql
SHOW EVENTS
    [LIKE | WHERE];
```
![scr1](/img2/.png)










- [Volver  a raíz](https://github.com/razielium7/MySQL_practice/blob/master/README.md)
