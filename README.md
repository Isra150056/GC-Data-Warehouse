# Marketing Intelligence Engine

## Prerequisitos
- Docker + Docker Compose v2
- Acceso al VPS o Codespace

## Primer despliegue

1. Clonar repo:
```bash
git clone https://github.com/Isra150056/GC-Data-Warehouse.git
cd GC-Data-Warehouse
```

2. Crear `.env` desde el ejemplo:
```bash
cp .env.example .env
```

3. Generar `N8N_ENCRYPTION_KEY`:
```bash
echo "N8N_ENCRYPTION_KEY=$(openssl rand -hex 32)" >> .env
```

4. Crear directorios con permisos correctos:
```bash
mkdir -p postgres/data n8n/data backups
```

5. Levantar servicios:
```bash
docker compose up -d
docker compose logs -f
```

6. Acceder a n8n:
- Local: http://localhost:5678
- Codespace: usa el botón "Open in Browser" del puerto 5678

## Acceso a pgAdmin (cuando lo necesites)

```bash
docker compose -f docker-compose.admin.yml up -d
# Luego accede al puerto 5050
```

## Comandos útiles

```bash
docker compose ps                    # Estado
docker compose logs -f n8n           # Logs de n8n
docker compose restart n8n           # Reiniciar servicio
docker compose down                  # Detener todo
```

## Backups

Los backups automáticos se guardan en `./backups/` con retención de 7 días, 4 semanas, 3 meses.

## Estructura del proyecto

```
.
├── docker-compose.yml          # Servicios principales
├── docker-compose.admin.yml    # pgAdmin (opcional)
├── .env.example                # Variables de entorno
├── postgres/init/init.sql      # Schema de la DB
├── pipeline/                   # Scripts de ingestión
└── README.md
```