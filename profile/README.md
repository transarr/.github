# Bienvenido a Transarr

Transarr es una plataforma para traducción, transcripción y gestión de subtítulos y medios, diseñada para integrarse fácilmente con herramientas como Bazarr y ofrecer una experiencia moderna y automatizada.

## ¿Qué puedes hacer aquí?
- Transcribir y traducir subtítulos automáticamente usando IA (Whisper, Argos Translate).
- Usar imágenes Docker listas para producción y pruebas.
- Integrar con Bazarr y otros sistemas de media.
- Gestionar flujos completos de subtitulado y traducción en varios idiomas.

## Uso rápido

### Usar la imagen Docker principal
```sh
docker run -d -p 5000:5000 ghcr.io/transarr/transarr-whisper:latest
```

### Stack completo (con UI)
```sh
docker compose up -d
```

- Accede a la UI en: http://localhost:3000
- API principal: http://localhost:5000

### Integración con Bazarr
Configura Bazarr para usar el endpoint:
```
http://localhost:5000
```

## Documentación técnica
- [Guía rápida y ejemplos](../docs/QUICKSTART.md)
- [Integración con Bazarr](../docs/BAZARR_INTEGRATION.md)
- [Arquitectura y MVP](../docs/Transarr_MVP_Spec.md)
- [Testing y buenas prácticas](../docs/TESTING.md)

## Licencia
MIT. Consulta el archivo LICENSE para más detalles.

---

¿Dudas o sugerencias? ¡Contribuye o abre un issue!
