# Repertorio musical CDFYV

Página web para registrar canciones de Alabanza y Adoración, guardar tonalidades, buscar, filtrar, editar, eliminar, detectar posibles duplicados y exportar a CSV.

## 1. Subir los archivos a GitHub

1. Descarga `index.html`.
2. Entra en https://github.com/Estbm26/CANCIONESCDFYV
3. Pulsa **Add file → Upload files**.
4. Arrastra `index.html` (y este `README.md` si también lo descargaste).
5. Escribe un mensaje como `Crear página inicial del repertorio`.
6. Pulsa **Commit changes**.

## 2. Publicar con GitHub Pages

1. En el repositorio entra en **Settings**.
2. En el menú izquierdo abre **Pages**.
3. En **Build and deployment**, selecciona **Deploy from a branch**.
4. En Branch selecciona **main** y carpeta **/(root)**.
5. Pulsa **Save**.
6. Espera unos minutos. GitHub mostrará la dirección pública de la página en esa misma sección de Pages.

## 3. Activar sincronización entre celulares y computadoras (Firebase)

Sin Firebase, la página funciona en modo local: los datos quedan guardados en ese navegador/dispositivo y no se comparten. Para que todos vean las mismas canciones:

1. Entra en https://console.firebase.google.com/ e inicia sesión.
2. Crea un proyecto, por ejemplo `repertorio-cdfyv`.
3. En el proyecto, agrega una aplicación web (icono `</>`). Registra la app y copia el objeto `firebaseConfig` que Firebase te muestra.
4. En Firebase, abre **Build → Authentication → Get started → Sign-in method** y activa **Anonymous**.
5. Abre **Build → Realtime Database → Create Database**. Elige la región y crea la base.
6. Copia la URL de Realtime Database que aparece en la consola (por ejemplo, `https://NOMBRE-default-rtdb.firebaseio.com` o la URL regional que te muestre Firebase).
7. En `index.html`, busca `const firebaseConfig = { ... }` y reemplaza los valores `PEGA_AQUI...` por los valores reales de tu configuración. No cambies los nombres de las propiedades.
8. En Realtime Database → **Rules**, coloca estas reglas iniciales y pulsa **Publish**:

```json
{
  "rules": {
    "songs": {
      ".read": "auth != null",
      ".write": "auth != null"
    }
  }
}
```

9. Guarda el `index.html` actualizado en GitHub (Add file → Upload files, o abre el archivo y usa el lápiz **Edit**). Haz **Commit changes**.
10. Abre la web publicada y prueba agregar una canción. Luego abre la página desde otro dispositivo para confirmar que aparece.

## Importante sobre permisos

Las reglas anteriores permiten que cualquier persona que pueda abrir la página y autenticarse anónimamente pueda leer y modificar el repertorio. Comparte el enlace solo con el equipo de música. Para un uso privado real, conviene implementar inicio de sesión individual y reglas por usuario antes de introducir información sensible.

## Funciones incluidas

- Registrar Alabanza o Adoración.
- Guardar tonalidad y persona que ingresó la canción.
- Buscar por nombre o persona.
- Filtrar por tipo y tonalidad.
- Ver canciones pendientes de tonalidad.
- Editar y eliminar.
- Aviso de posible canción duplicada.
- Exportar el repertorio a CSV.
- Diseño adaptable a celulares y computadoras.
