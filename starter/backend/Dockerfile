FROM public.ecr.aws/lambda/python:3.10

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /

RUN yum install -y \
    pcre \
    pcre-devel \
    gcc \
    gcc-c++ \
    make \
    openssl-devel \
    libffi-devel \
    python3-devel \
    && yum clean all \
    && pip install pipenv

RUN mkdir -p /var/www/app /app

COPY Pipfile* /app/

RUN cd /app && pipenv install --system --deploy

COPY . /app

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "-s", "/var/www/app/app.sock", "--manage-script-name", "--mount", "/=app:app"]