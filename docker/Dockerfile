FROM python:3.7
ENV PYTHONUNBUFFERED 1

RUN groupadd -g 999 user \
    && useradd -r -u 999 -g user user

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
    && pip install --no-cache-dir \
        uWSGI==2.0.18 \
        mysqlclient==1.4.4 \
    && apt-get purge -y build-essential

COPY requirements.txt conf /var/www/server/
RUN pip install --no-cache-dir -r /var/www/server/requirements.txt

COPY . /var/www/server/
WORKDIR /var/www/server

CMD ["/usr/local/bin/uwsgi", "--ini", "/var/www/server/conf/uwsgi.ini"]
EXPOSE 8000