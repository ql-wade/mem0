FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

# PAV2 patch: psycopg-binary（python:3.12-slim 缺 libpq → no pq wrapper）+ tsinghua pip 加速
RUN pip install --no-cache-dir psycopg-binary>=3.2.8 && \
    pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

ENV PYTHONUNBUFFERED=1

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
