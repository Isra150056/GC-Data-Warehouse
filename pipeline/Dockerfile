FROM python:3.13-slim

COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

WORKDIR /code

ENV PATH="/code/.venv/bin:$PATH" \
    PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    UV_LINK_MODE=copy

COPY pyproject.toml .python-version ./
RUN uv sync --locked --no-dev

COPY *.py ./

ENTRYPOINT ["python", "ingest_data.py"]