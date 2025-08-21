<div align="center">

# 🌸✨ PostgreSQL Kawaii Guide ✨🌸

*La guía más adorable para dominar PostgreSQL con Docker* 💕



*¡Aprende PostgreSQL de la forma más kawaii posible!* (´｡• ᵕ •｡`) ♡

</div>

---

## 🎯 ¿Qué encontrarás aquí?

<table>
<tr>
<td align="center">🐳</td>
<td><strong>Docker Setup</strong><br/>Configuración súper fácil con Docker</td>
</tr>
<tr>
<td align="center">💎</td>
<td><strong>SQL Kawaii</strong><br/>Ejemplos adorables de consultas SQL</td>
</tr>
<tr>
<td align="center">🏗️</td>
<td><strong>Database Design</strong><br/>Estructuras bonitas y bien organizadas</td>
</tr>
<tr>
<td align="center">⚡</td>
<td><strong>Quick Commands</strong><br/>Comandos rápidos para ser productivo</td>
</tr>
</table>

---

## 🚀 Quick Start

### 1. 🐳 Crear tu contenedor PostgreSQL

```bash
docker run -d \
  --name=postgres_kawaii 🌸 \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=admin \
  -e POSTGRES_DB=campus \
  -p 5433:5432 \
  -v pgdata:/var/lib/postgresql/data \
  --restart=unless-stopped \
  postgres:15
```

### 2. 🔗 Conectarse

```bash
# Entrar al contenedor
docker exec -it postgres_kawaii sh

# Conectar con PostgreSQL
psql -h localhost -U admin -d campus -W
```

---

## 🎀 Comandos Esenciales

<details>
<summary>🔍 <strong>Exploración de Base de Datos</strong></summary>

```sql
\l                    -- 📋 Listar bases de datos
\c database_name      -- 🔄 Cambiar de base de datos
\dt                   -- 🏠 Ver tablas
\d table_name         -- 🔍 Describir tabla específica
```
</details>

<details>
<summary>🏗️ <strong>Gestión de Estructura</strong></summary>

```sql
\ds                   -- 🔢 Ver secuencias
\di                   -- 📇 Ver índices
\dn                   -- 🏗️ Ver esquemas
\dp                   -- 🔐 Ver privilegios
```
</details>

---

## 💎 Ejemplos Kawaii

### 🦄 Tipos Personalizados

```sql
-- ✨ Creando un tipo enum adorable ✨
CREATE TYPE estado_civil AS ENUM('soltero', 'casado', 'complicado');

CREATE TABLE usuarios(
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    estado estado_civil DEFAULT 'soltero'
);
```

### 🌈 Tabla con Todos los Tipos

```sql
-- 🎀 La tabla más completa del universo kawaii 🎀
CREATE TABLE productos_kawaii (
    id SERIAL PRIMARY KEY,                    -- 🔑 ID único
    nombre VARCHAR(100) NOT NULL,             -- 📛 Nombre del producto
    descripcion TEXT,                         -- 📝 Descripción detallada
    precio NUMERIC(10,2) NOT NULL,            -- 💰 Precio exacto
    en_stock BOOLEAN DEFAULT true,            -- ✅ ¿Disponible?
    fecha_creacion DATE DEFAULT CURRENT_DATE, -- 📅 Cuándo se creó
    colores VARCHAR(20)[],                    -- 🌈 Array de colores
    datos_extra JSONB,                        -- 🚀 Datos flexibles
    codigo UUID DEFAULT gen_random_uuid()     -- 🆔 Código único
);
```

### 💫 Constraints Kawaii

```sql
-- 🔒 Agregando restricciones adorables 🔒

-- Primary Key
ALTER TABLE empleados ADD PRIMARY KEY(id);

-- Foreign Key con nombre bonito
ALTER TABLE empleados 
ADD CONSTRAINT fk_empleado_departamento 
FOREIGN KEY(departamento_id) 
REFERENCES departamentos(id);

-- Unique constraint
ALTER TABLE productos 
ADD CONSTRAINT uk_producto_nombre UNIQUE(nombre);

-- Check constraint para validaciones
ALTER TABLE empleados 
ADD CONSTRAINT ck_edad_minima CHECK (edad >= 18);

-- Default values
ALTER TABLE empleados 
ALTER COLUMN salario SET DEFAULT 1000.00;
```

---

## 🎯 Consultas Kawaii Avanzadas

### 🏆 Top Productos Más Vendidos

```sql
SELECT 
    p.nombre,
    SUM(cp.cantidad) AS unidades_vendidas,
    SUM(cp.total) AS ingresos_totales,
    '🌟' AS estrella
FROM productos p
JOIN compras_productos cp ON p.id = cp.id_producto
GROUP BY p.id, p.nombre
ORDER BY unidades_vendidas DESC
LIMIT 10;
```

### 📊 Estadísticas de Ventas

```sql
-- 🧮 Análisis kawaii de ventas 🧮
WITH ventas_diarias AS (
    SELECT 
        DATE(fecha) as dia,
        SUM(total) as venta_dia
    FROM compras
    GROUP BY DATE(fecha)
)
SELECT 
    '📈 Promedio' as metrica,
    ROUND(AVG(venta_dia), 2) as valor
FROM ventas_diarias
UNION ALL
SELECT 
    '📊 Mediana' as metrica,
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY venta_dia) as valor
FROM ventas_diarias;
```

### 🔍 Búsqueda Inteligente

```sql
-- ☕ Buscar productos que empiecen con 'caf' ☕
SELECT 
    nombre,
    precio,
    CASE 
        WHEN cantidad_stock > 10 THEN '✅ Bien surtido'
        WHEN cantidad_stock > 0 THEN '⚠️ Poco stock'
        ELSE '❌ Agotado'
    END as estado_stock
FROM productos
WHERE nombre ILIKE 'caf%'
  AND estado = 'activo'
ORDER BY cantidad_stock DESC;
```

---

## 🛠️ Funciones Útiles

### 💝 Función para Calcular Total de Compra

```sql
CREATE OR REPLACE FUNCTION calcular_total_compra(p_id_compra INT)
RETURNS NUMERIC 
LANGUAGE plpgsql AS $
DECLARE  
    v_total NUMERIC(16,2) := 0;
BEGIN
    SELECT COALESCE(SUM(total), 0)
    INTO v_total
    FROM compras_productos
    WHERE id_compra = p_id_compra;

    RETURN v_total;
END;
$;
```

### 🎯 Uso de la Función

```sql
-- 💫 Calculando el total de la compra #123
SELECT calcular_total_compra(123) as total_kawaii;
```

---

## 🏋️‍♀️ Ejercicios Prácticos

### 🌍 Estructura Geográfica

```sql
-- Crear las tablas base
CREATE TABLE paises (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    codigo_iso CHAR(2) UNIQUE
);

CREATE TABLE regiones (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    id_pais INTEGER REFERENCES paises(id)
);

CREATE TABLE ciudades (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    id_region INTEGER REFERENCES regiones(id)
);
```

**🎯 Tu misión:** Agregar todas las constraints usando `ALTER TABLE`

---

## 🎉 Tips Kawaii

> 💡 **Consejo #1:** Siempre usa nombres descriptivos para tus constraints
> 
> 💡 **Consejo #2:** Los comentarios en SQL también pueden ser kawaii
> 
> 💡 **Consejo #3:** Usa `COALESCE()` para manejar valores NULL de forma elegante

---

## 📚 Recursos Adicionales

- 📖 [Documentación Oficial PostgreSQL](https://www.postgresql.org/docs/)
- 🐳 [Docker Hub - PostgreSQL](https://hub.docker.com/_/postgres)
- 💡 [Mejores Prácticas SQL](https://example.com)

---

<div align="center">

### 🌸 ¡Gracias por usar esta guía! 🌸

*Si te gustó, no olvides darle una ⭐ al repo*

**Hecho con mucho 💕 y código kawaii**

---

*¿Encontraste algún error? ¡Abre un issue y lo arreglaremos juntos!* ✨

</div>