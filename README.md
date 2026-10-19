# ETL Seiri Perú — Data Warehouse

Proyecto del curso Business Intelligence (ESAN). ETL en SSIS que construye
el Data Warehouse **SeiriDW** a partir de la base transaccional **SeiriDB**.

## Preparación (una sola vez)
1. Ejecutar `BaseDatos/SeiriDB_Script.sql` en SSMS (F5). Crea SeiriDB con 17 tablas.
2. Crear el DW vacío: `CREATE DATABASE SeiriDW;`
3. Abrir `ETL_SeiriDW.sln` en Visual Studio.
4. Si una conexión falla: doble clic en el .conmgr → servidor `localhost`,
   Trust Server Certificate = True, Use Encryption for Data = False.

## Reglas
- Cada persona trabaja SOLO su paquete. No modificar otros paquetes ni el Orquestador.
- Tablas del DW: DimFecha, DimProducto, DimCliente, DimComprobante, DimAlmacen,
  DimTipoMovimiento, FactVentas, FactInventario (se crean con "Nuevo" en el Destino OLE DB).
- Llaves de las Dim = los Id de SeiriDB. DimFecha usa IdFecha entero AAAAMMDD.
- Cada paquete inicia con una Tarea Ejecutar SQL que vacía su tabla:
  `IF OBJECT_ID('dbo.NombreTabla') IS NOT NULL TRUNCATE TABLE dbo.NombreTabla;`
- Qué limpiar y qué técnicas usar: `BaseDatos/SeiriDB_Documentacion.xlsx`
  (hojas Calidad_y_ETL y Mapa_al_DW).

## Responsables
| Paquete | Responsable |
|---|---|
| CargaDimFecha, CargaDimComprobante, CargaDimAlmacen, CargaDimTipoMovimiento | Italo |
| CargaDimCliente | Nahim |
| CargaDimProducto, CargaFactInventario | Joaquín |
| CargaFactVentas, Orquestador | Sebastián |
| SeiriDB, proyecto base e integración | Cielo |