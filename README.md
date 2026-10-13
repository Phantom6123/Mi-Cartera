# Mi Cartera

App web (PWA) para llevar ingresos, gastos y la proyección de cuánto necesitas ganar cada mes.

- `index.html`: toda la app (HTML, CSS y JS sin dependencias).
- `manifest.webmanifest`, `icon.svg`, `sw.js`: permiten instalarla en el móvil y usarla sin conexión.

Los datos se guardan en el navegador (localStorage, clave `micartera.v1`). No se sincronizan entre dispositivos; usa Ajustes → Copia de seguridad para pasarlos.

Para probarla en local: `python3 -m http.server` dentro de esta carpeta y abre http://localhost:8000.

## Sincronización

Publicada como Artifact en claude.ai (https://claude.ai/artifact/LEsASNsGxX6f9Xkvu2Eatw), la app usa la base de datos privada del Artifact (`data/users/<id>/`: documento `config` + un documento `m-AAAA-MM` por mes con sus movimientos) y se sincroniza entre dispositivos con la cuenta de Claude. Abierta fuera de claude.ai, funciona solo con localStorage.

## Versión independiente (GitHub Pages + Firebase)

1. Crea un proyecto en https://console.firebase.google.com (plan gratuito Spark).
2. Authentication → Sign-in method → activa **Google**. En Authentication → Settings → Authorized domains añade `<usuario>.github.io`.
3. Firestore Database → Crear base de datos (modo producción) y pega las reglas de `firestore.rules`.
4. Configuración del proyecto → Tus apps → Web (</>) → copia el objeto `firebaseConfig` en `config.js` (`window.FIREBASE_CONFIG = {...}`). Estos datos no son secretos; la seguridad la dan las reglas.
5. Sube esta carpeta a un repositorio de GitHub y activa Pages (Settings → Pages → rama `main`, carpeta raíz).

Datos en Firestore: `users/<uid>/docs/config` y `users/<uid>/docs/m-AAAA-MM`.
