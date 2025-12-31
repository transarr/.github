# Welcome to Transarr

Transarr is a platform for transcription, translation, and subtitle/media management, designed to integrate easily with tools like Bazarr and provide a modern, automated experience.

## What you can do here
- Transcribe and translate subtitles automatically using AI (Whisper, Argos Translate).
- Use Docker images ready for production and testing.
- Integrate with Bazarr and other media systems.
- Manage full subtitle and translation workflows across multiple languages.

## Quickstart

### Run the main Docker image
```sh
docker run -d -p 5000:5000 ghcr.io/transarr/transarr-whisper:latest
```

### Full stack with UI
```sh
docker compose up -d
```

- UI: http://localhost:3000
- API: http://localhost:5000

### Bazarr integration
Configure Bazarr to use the endpoint:
```
http://localhost:5000
```

## Technical docs
- [Quickstart and examples](../docs/QUICKSTART.md)
- [Bazarr integration](../docs/BAZARR_INTEGRATION.md)
- [Architecture and MVP](../docs/Transarr_MVP_Spec.md)
- [Testing and best practices](../docs/TESTING.md)

## License
MIT. See the `LICENSE` file at the project root for details.

---

Questions or suggestions? Contribute or open an issue!
