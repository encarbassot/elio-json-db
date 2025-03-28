# Elio JSON DB

Elio JSON DB es una base de datos simple basada en archivos JSON, que permite realizar operaciones CRUD de manera estructurada con validaciones de esquema, autoincremento, valores por defecto y funciones de actualización.

## Instalación como submódulo

Si deseas usar este repositorio como un submódulo en tu proyecto, sigue estos pasos:

```bash
# Dentro del directorio de tu proyecto
git submodule add https://github.com/encarbassot/elio-json-db elio-json-db
```
Luego, clona los submódulos cuando descargues el repositorio:
```bash
git submodule update --init --recursive
```

Si deseas actualizar el submódulo a la última versión:

```bash
cd elio-json-db
git pull origin main
cd ..
```

## Uso

### Importación y configuración

```js
import JsonDB from './elio-json-db/JsonDB.js';

export const db = new JsonDB({
  menus: {
    id: { type: "string", primary: true, unique: true, autoIncrement: true },
    title: { type: "string", notNull: true },
    description: { type: "string", notNull: true },
    emoji: { type: "string", notNull: true, default: "🍎" },
    created_at: { type: "string", default: () => new Date().toISOString() },
    updated_at: { type: "string", onUpdate: () => new Date().toISOString() }
  }
});
```

### Operaciones CRUD

Insertar registros

```js
db.insert("menus", { title: "Desayuno", description: "Menú de la mañana" });
```

### Consultar registros

```js
const menus = db.find("menus");
const menu = db.findOne("menus", { title: "Desayuno" });
```

### Actualizar registros

```js
db.update("menus", { description: "Menú de la mañana actualizado" }, { title: "Desayuno" });
```

### Eliminar registros

```js
db.delete("menus", { title: "Desayuno" });
```

### Características

- Esquema de datos configurable

- Validación de tipos y restricciones (notNull, unique, primary key)

- Campos autoincrementales

- Funciones de actualización automática (onUpdate)

- Almacenamiento en un único archivo JSON
