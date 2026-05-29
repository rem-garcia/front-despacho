#  Front Despacho — Innovatech Chile

Frontend de la aplicación de gestión de despachos, desarrollado con React + Vite y desplegado en AWS EC2 mediante un pipeline CI/CD automatizado con GitHub Actions.

##  Tecnologías utilizadas

- React 18
- Vite 5
- Tailwind CSS
- Axios
- Docker (multi-stage build)
- Nginx
- GitHub Actions (CI/CD)
- Amazon EC2 + SSM

##  Estructura del proyecto

front_despacho/
├── .github/
│   └── workflows/
│       └── cicd-frontend.yml   # Pipeline CI/CD
├── src/                        # Código fuente React
├── public/                     # Assets estáticos
├── Dockerfile                  # Multi-stage build
├── docker-compose.yml          # Stack local
└── README.md

##  Cómo ejecutar localmente

### Pre-requisitos
- Docker Desktop instalado y corriendo

### Pasos

1. Clonar el repositorio
```bash
git clone https://github.com/rem-garcia/front-despacho.git
cd front-despacho
```

2. Construir y levantar el contenedor
```bash
docker compose up -d
```

3. Abrir en el navegador

http://localhost:80

4. Para detener
```bash
docker compose down
```

##  Pipeline CI/CD

El pipeline se activa automáticamente con cada push a la rama `deploy` y realiza los siguientes pasos:

1. **Build** — construye la imagen Docker multi-stage
2. **Push** — publica la imagen en Docker Hub (`remiale/front-despacho:latest`)
3. **Deploy** — via AWS SSM envía comandos a la EC2 para descargar y levantar el nuevo contenedor

##  Despliegue en AWS

- **EC2 Frontend:** `http://34.234.76.180`
- **Puerto:** 80
- **Imagen Docker Hub:** `remiale/front-despacho:latest`

##  Secrets requeridos en GitHub Actions

| Secret | Descripción |
|--------|-------------|
| `AWS_ACCESS_KEY_ID` | Credencial AWS |
| `AWS_SECRET_ACCESS_KEY` | Credencial AWS |
| `AWS_SESSION_TOKEN` | Token de sesión AWS Academy |
| `AWS_REGION` | Región AWS (us-east-1) |
| `EC2_FRONTEND_INSTANCE_ID` | ID de la instancia EC2 |
| `DOCKERHUB_USERNAME` | Usuario Docker Hub |
| `DOCKERHUB_TOKEN` | Token de acceso Docker Hub |