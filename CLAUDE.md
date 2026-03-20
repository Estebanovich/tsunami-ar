# Tsunami AR — Feria de Ciencias

Proyecto de realidad aumentada web (sin app) para una feria de ciencias sobre tsunamis.
El visitante escanea un QR → abre una página web → apunta la cámara al marcador Hiro → ve el video del tsunami en AR.

## Stack

- **AR.js** — detección de marcadores en el navegador
- **A-Frame** — escena 3D/AR
- **Marcador:** Hiro (preset incluido en AR.js)
- **Video:** `tsunami.mp4` (H.264, 720p, <15MB)
- **Hosting:** GitHub Pages (HTTPS obligatorio para acceso a cámara)

## Estructura del proyecto

```
/
├── index.html        # Escena AR principal
├── tsunami.mp4       # Video del tsunami (asset principal)
├── marker-hiro.jpg   # Imagen del marcador para imprimir
└── README.md
```

## Comandos frecuentes

```bash
# Servidor local para desarrollo (HTTPS necesario para cámara)
npx serve . --ssl-cert cert.pem --ssl-key key.pem

# Comprimir video con ffmpeg
ffmpeg -i input.mp4 -vcodec h264 -acodec aac -vf scale=1280:720 tsunami.mp4

# Deploy a GitHub Pages
git add . && git commit -m "update" && git push origin main
```

## Convenciones

- El video debe tener `autoplay loop playsinline webkit-playsinline` para funcionar en iOS
- El marcador Hiro debe imprimirse en A4, mínimo 10×10 cm, sobre superficie plana
- La página debe servirse siempre por HTTPS (requerimiento del navegador para webcam)
- No agregar dependencias adicionales — AR.js + A-Frame via CDN es suficiente

## Restricciones conocidas

- **iOS Safari:** requiere `webkit-playsinline` en el tag `<video>` — ya incluido
- **Android Chrome:** funciona sin configuración extra
- **Iluminación:** el marcador necesita buena luz para ser detectado
- **Video pesado:** si supera 20MB, comprimir antes de subir

## Archivos de referencia

- Código base AR: `index.html`
- Marcador Hiro oficial: https://ar-js-org.github.io/AR.js/data/images/HIRO.jpg
- Docs AR.js: https://ar-js-org.github.io/AR.js-Docs/

## Contexto del proyecto

Feria de ciencias escolar. La audiencia son visitantes que no descargarán ninguna app.
El flujo completo es: QR impreso → URL pública → página web → cámara → marcador Hiro → video AR.
Priorizar simplicidad y compatibilidad cross-browser sobre efectos visuales complejos.
