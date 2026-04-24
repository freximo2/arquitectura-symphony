# Symphony · AI Platform Engineering

Presentación técnica en una sola página HTML para el diseño de plataforma **Symphony** (AI-first, banca regulada): arquitectura por capas, golden path del agente, decisiones de arquitectura, observabilidad y roadmap a 12 meses.

## Contenido del repositorio

| Archivo | Rol |
|--------|-----|
| `index.html` | SPA estática: barra lateral con 5 secciones (Arquitectura, Golden Path, Decisiones, Observabilidad, Visión 12 meses), estilos embebidos y navegación por JavaScript. Tema oscuro, tipografías Google (Syne, Inter, DM Mono). Describe GCP, Kong AI Gateway, LangGraph, Vertex AI, Redis/Firestore, MCP por dominio, BIAN, SLIs y runbooks. |
| `Dockerfile` | Imagen `nginx:alpine` que copia `index.html` a `/usr/share/nginx/html` y expone el puerto **80**. |
| `README.md` | Este archivo. |

El ZIP original de distribución está en `archive/files.zip` por si necesitas el paquete tal cual se entregó.

## Ejecución con Docker

Los 3 archivos van en la misma carpeta (el contexto de build debe incluir `Dockerfile` e `index.html` juntos).

```bash
docker build -t symphony-platform .
docker run -p 8080:80 symphony-platform
```

Abrir: **http://localhost:8080**

Para detener el contenedor:

```bash
docker stop $(docker ps -q --filter ancestor=symphony-platform)
```

## Estructura del repositorio

```
arquitectura-symphony/
├── index.html
├── Dockerfile
├── README.md
└── archive/
    └── files.zip
```

## Secciones de la presentación (`index.html`)

| # | Sección | Contenido resumido |
|---|---------|---------------------|
| 01 | Arquitectura | Cuatro capas (DX/IDP, governance/Kong, orquestación LangGraph, infra GCP) más capa externa core banking; foco en Kong + LangGraph y agente Personal Banker. |
| 02 | Golden Path | Ocho pasos desde scaffolding hasta producción con gates de compliance y despliegue canario. |
| 03 | Decisiones | Tres trade-offs: Redis+Firestore, Kong vs gateways genéricos, MCP por dominio vs centralizado. |
| 04 | Observabilidad | SLIs/SLOs, drift y hallucination, checkpointing, runbook P1. |
| 05 | Visión 12 meses | Tres horizontes, KPIs, riesgos y build vs buy. |

## Publicar en GitHub Pages (opcional)

1. Subir los archivos al repositorio (en la raíz del sitio).
2. **Settings → Pages** → origen: rama (por ejemplo `main`) y carpeta `/ (root)`.
3. Tras el despliegue, la URL será `https://<usuario>.github.io/<repositorio>`.

Para Pages solo hace falta servir `index.html`; Docker es útil para previsualizar igual que en producción con nginx.
