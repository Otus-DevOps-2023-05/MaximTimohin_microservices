FROM python:3.6.0-alpine

RUN apk add --no-cache --virtual .build-deps gcc musl-dev libffi-dev openssl-dev make

WORKDIR /app

ADD . /app

RUN pip install -v -r /app/requirements.txt

RUN apk del .build-deps

ENV POST_DATABASE_HOST=post_db POST_DATABASE=posts

CMD ["python3", "post_app.py"]
