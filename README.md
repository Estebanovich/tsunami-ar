# Tsunami AR — Feria de Ciencias

Experiencia de realidad aumentada web sobre tsunamis. Sin app, solo escanear un QR.

## Flujo de uso

1. El visitante escanea el QR impreso
2. Se abre la página en el navegador
3. El navegador pide permiso de cámara → aceptar
4. Apuntar la cámara al **marcador Hiro** impreso
5. El video del tsunami aparece en AR sobre el marcador

## Marcador Hiro

Imprimir en A4, mínimo **10×10 cm**, sobre superficie plana y bien iluminada.

Imagen oficial: https://ar-js-org.github.io/AR.js/data/images/HIRO.jpg

## Archivos necesarios

| Archivo | Descripción |
|---------|-------------|
| `index.html` | Escena AR principal |
| `tsunami.mp4` | Video del tsunami (H.264, 720p, <15MB) |

## Desarrollo local

Se requiere HTTPS para acceder a la cámara.

```bash
# Opción 1: npx serve con SSL
npx serve . --ssl-cert cert.pem --ssl-key key.pem

# Opción 2: desde otro dispositivo en la misma red
npx serve .
# Luego acceder desde https://<IP-local>:3000 (usar ngrok si es necesario)
```

## Deploy

```bash
git add .
git commit -m "update"
git push origin main
```

GitHub Pages sirve automáticamente por HTTPS desde la rama `main`.

## Comprimir video (si supera 20MB)

```bash
ffmpeg -i input.mp4 -vcodec h264 -acodec aac -vf scale=1280:720 tsunami.mp4
```

## Compatibilidad

- **iOS Safari:** funciona (incluye `webkit-playsinline`)
- **Android Chrome:** funciona sin configuración extra
- **Desktop Chrome/Firefox:** funciona con webcam
