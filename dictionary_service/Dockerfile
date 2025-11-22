FROM python:3.9-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    && rm -rf /var/lib/apt/lists/*

COPY dictionary_service/requirements.txt .
COPY protobufs/ /app/protobufs/

RUN pip install --no-cache-dir -r requirements.txt

RUN python -m grpc_tools.protoc -I /app/protobufs \
    --python_out=/app \
    --grpc_python_out=/app \
    /app/protobufs/dictionary.proto

COPY dictionary_service/ /app/

RUN mkdir -p /var/log/app

EXPOSE 50051

CMD ["python", "server.py"]