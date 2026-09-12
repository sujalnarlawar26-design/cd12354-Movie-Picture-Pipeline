FROM public.ecr.aws/lambda/python:3.10

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

COPY Pipfile* ./

RUN pip install --no-cache-dir pipenv && \
    pipenv install --system --deploy

COPY . .

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "-s", "/var/www/app/app.sock", "--manage-script-name", "--mount", "/=app:app"]