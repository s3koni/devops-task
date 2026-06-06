FROM python:3.12-alpine

WORKDIR /app

COPY app.py .

RUN adduser -D appuser

RUN apk add --no-cache wget

USER appuser

EXPOSE 8080

CMD ["python", "app.py"]
