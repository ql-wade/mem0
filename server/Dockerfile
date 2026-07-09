FROM python:3.12-slim

WORKDIR /app

# Context = repo root（含 mem0/ + server/），所以路径用 server/...
COPY server/requirements.txt .

# PAV2 patch: psycopg-binary（python:3.12-slim 缺 libpq → no pq wrapper）
RUN pip install --no-cache-dir psycopg-binary>=3.2.8 && \
    pip install --no-cache-dir -r requirements.txt

# 复制 server 源码 + mem0 fork 源码（patches）
COPY server/ /app/
COPY mem0/ /app/mem0/

# PAV2 patch: bake mem0 fork source over PyPI-installed mem0ai
# (response_format retry + 其他兼容性 fix)
RUN cp -r /app/mem0/* /usr/local/lib/python3.12/site-packages/mem0/

EXPOSE 8000

ENV PYTHONUNBUFFERED=1

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
