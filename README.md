# ETL Seiri Perú — Data Warehouse

Proyecto del curso Business Intelligence (ESAN). ETL en SSIS que construye
el Data Warehouse **SeiriDW** a partir de la base transaccional **SeiriDB**.

📘 **Guía completa del proyecto (qué hace cada uno y qué busca cada tabla):**
[https://docs.google.com/document/d/1Uyz8O7wSTE32sKI-o6WVibDk_xDTU3WJ/edit?usp=drive_link&ouid=113173398818376245069&rtpof=true&sd=true]

## Preparación (una sola vez)
1. Aceptar la invitación de GitHub que llega al correo y clonar este repositorio.
2. Ejecutar `BaseDatos/SeiriDB_Script.sql` en SSMS (F5). Crea SeiriDB con 17 tablas.
3. Crear el DW vacío en SSMS: `CREATE DATABASE SeiriDW;`
4. Abrir `ETL_SeiriDW.slnx` en Visual Studio.
5. Si una conexión falla: doble clic en el .conmgr → servidor `localhost`,
   Trust Server Certificate = True, Use Encryption for Data = False.
6. Si sale un error de versión al abrir el proyecto, avisar a Cielo antes de tocar nada.

## Reglas
- Antes de empezar: Git → Extraer (pull). Trabajar SOLO el paquete propio.
- No modificar otros paquetes, el Orquestador ni el archivo .dtproj.
- Nombres de tablas y columnas: exactamente los de la guía.
- Cada paquete: Tarea Ejecutar SQL "Borrar <Tabla>" → Tarea Flujo de datos "Cargar <Tabla>".
- Todas las tablas del DW llevan la columna FechaCarga = GETDATE().
- Al terminar: ejecutar la consulta de comprobación de la guía. Si no cuadra, no subir.
- Subir solo el .dtsx propio, con el mensaje "<Tabla>: carga completa".

## Responsables
| Paquete | Responsable |
|---|---|
| SeiriDB, proyecto base, Orquestador e integración final | Cielo |
| CargaDimFecha, CargaDimComprobante | Italo |
| CargaDimCliente, CargaDimAlmacen, CargaDimTipoMovimiento | Nahim |
| CargaDimProducto, CargaFactInventario | Joaquín |
| CargaFactVentas y validación final | Sebastián |

## Orden de carga
1. Dimensiones (en paralelo): DimFecha, DimProducto, DimCliente, DimComprobante, DimAlmacen, DimTipoMovimiento
2. Hechos: FactVentas, FactInventario
3. Validación final y ejecución del Orquestador completo
