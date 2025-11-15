# DEMO-DEVFEST-TARIJA

# 1. Flujo del taller

1. Preparar entorno
2. Generar la app usando IA (fase con datos mock)
3. Ejecutar y revisar la version mock
4. Pedir a IA la version conectada con Spotify
5. Añadir una mejora personalizada
6. Ejecutar con datos reales
7. Desplegar a Vercel

---

# 2. Requisitos

* Node.js 18 o superior
* Git
* Navegador actualizado
* Cuenta de Google (para Google AI Studio)
* Cuenta de Spotify (opcional pero recomendada)

---

# 3. Preparar Google AI Studio

Antes de generar el proyecto, debemos indicarle a la IA como queremos que construya la aplicacion.

Entra a:
Google AI Studio -> Build -> Advanced Settings -> System Instructions

Copia el siguiente texto:

```
You generate modern Angular applications using clean, maintainable and production-ready code.

Rules:
- Use standalone components.
- Use Angular Material for UI.
- Organize the project into components, services, and assets.
- Include a sample-data.json file with mock music tracks, artists, and audio_features.
- Include .env.example with placeholders.
- Ensure the project compiles with `npm install && ng serve`.
- Avoid deprecated APIs.
- Provide clear comments and mark sections with "Customize here".
```

---

# 4. Primera generacion con IA (modo mock)

Primero generaremos una version que usa datos falsos. Esto permite revisar la estructura de la app antes de trabajar con Spotify.

Pega este prompt en la caja principal del editor:

```
Generate an Angular application called "My Spotify Wrap-Up".

Requirements:
- Use mock data only.
- Include sample-data.json with tracks, artists, and audio features.
- Components: Login (inactive), Dashboard, TopTracks, TopArtists, AudioFeatures.
- Services: DataService to load mock data.
- Use Angular Material for layout.
- Responsive design.
- Add a README explaining how to run the app.
```

Ejecuta "Run" y descarga el ZIP o exportalo a GitHub.

---

# 5. Ejecutar la version mock

1. Clona tu repositorio o descomprime el ZIP.
2. Instala dependencias:

```
npm ci
```

3. Ejecuta:

```
npm run start:mock
```

Abre en el navegador:
[http://localhost:4200](http://localhost:4200)

Debes ver un Wrap-Up funcional con datos ficticios.

Este modo funciona incluso sin internet y te permite entender la base del proyecto.

---

# 6. Revisar tu app generada

Observa lo siguiente:

* Como se ve el dashboard
* Como se presentan las canciones y artistas
* Que informacion te gustaria ver en tu propio Wrap-Up
* Que mejoras agregarias si pudieras decidir una funcionalidad personalizada

Estos puntos te ayudaran en la fase creativa mas adelante.

---

# 7. Segunda generacion con IA: integrar Spotify API

Cuando ya hayas probado la version mock, pediremos a la IA que genere la version que integra la API real de Spotify.

Copia este prompt en Google AI Studio:

```
Take the previous project you generated and upgrade it.

Replace the mock data with the real Spotify Web API using OAuth 2.0 PKCE.

Requirements:
- Add AuthService implementing PKCE flow.
- Add SpotifyApiService with endpoints: getMe, getTopTracks, getTopArtists, getAudioFeatures.
- Keep the mock mode as fallback using sample-data.json.
- Add .env.example with SPOTIFY_CLIENT_ID, SPOTIFY_REDIRECT_URI, USE_PROXY.
- Include an AuthInterceptor to attach the token.
- Maintain the same UI and components.
```

Ejecuta "Run" y exporta la nueva version de tu proyecto.

---

# 8. Conectar tu app con Spotify

## 1. Crear la app en Spotify

1. Ve a [https://developer.spotify.com/dashboard](https://developer.spotify.com/dashboard)
2. Inicia sesion
3. Clic en "Create an App"
4. Coloca un nombre, por ejemplo:
   WrapUp-DevFest-TuNombre
5. En "Redirect URIs", agrega:

```
http://localhost:4200/callback
```

Guarda los cambios y copia tu Client ID.

## 2. Configurar `.env`

Edita tu archivo `.env`:

```
SPOTIFY_CLIENT_ID=TU_CLIENT_ID
SPOTIFY_REDIRECT_URI=http://localhost:4200/callback
USE_PROXY=false
```

## 3. Ejecutar la app

```
npm run start:local
```

Presiona "Login with Spotify" y autoriza.

Si funciona, veras tus datos reales. Si no, activa el proxy:

```
USE_PROXY=true
PROXY_URL=https://<url-del-proxy-del-taller>/exchange-token
```

Luego vuelve a intentar.

---

# 9. Crear tu propia mejora personalizada con IA

Esta parte es creativa. Tu decides que funcion extra quieres.

Ideas comunes:

* Mostrar tu top de generos
* Calcular la energia promedio de tus canciones
* Ordenar tus tracks por BPM
* Crear tu playlist personalizada "Week Recap"
* Comparar tu gusto musical entre periodos corto, mediano y largo
* Un "perfil musical" basado en tus datos

Prompt sugerido:

```
Add a new feature to my Spotify Wrap-Up app.

I want to include: <describe your idea here>.

Requirements:
- Create a new component named <NameOfFeature>.
- Add any required calculations in the service layer.
- Use Angular Material for the UI.
- Keep the style consistent.
- Use data from getTopTracks, getTopArtists, or audio-features.
```

Integra el codigo generado a tu proyecto.

---

# 10. Deploy a Vercel

1. Sube tu repo a GitHub
2. Entra a [https://vercel.com](https://vercel.com)
3. Importa tu proyecto
4. Agrega variables de entorno:

```
SPOTIFY_CLIENT_ID=<tu id>
SPOTIFY_REDIRECT_URI=https://<tu-app>.vercel.app/callback
USE_PROXY=true
PROXY_URL=https://<url-del-proxy>
```

5. Ejecuta el deploy
6. Agrega tu nueva URL a los Redirect URIs de Spotify:

```
https://<tu-app>.vercel.app/callback
```

Tu app ya esta publica.

---

# 11. Troubleshooting

Problema: "Redirect URI mismatch"
Solucion: debe coincidir exactamente con el valor configurado en Spotify.

Problema: CORS
Solucion: activar USE_PROXY=true.

Problema: La app no compila
Solucion: verificar Node 18 o reinstalar dependencias con `npm ci`.

Problema: Login funciona pero no salen datos
Solucion: volver a iniciar sesion y revisar permisos.

---

# 12. Conclusiones

En este taller aprendiste a:

* Generar una app con Google AI Studio
* Empezar con datos mock para revisar la UI
* Integrar la API real de Spotify usando OAuth PKCE
* Añadir una funcionalidad personalizada usando IA
* Desplegar tu app con Vercel
