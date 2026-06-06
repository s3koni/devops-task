FROM python:3.12-alpine

WORKDIR /app

COPY app.py .

RUN adduser -D appuser

USER appuser

EXPOSE 8080

CMD ["python", "app.py"]
