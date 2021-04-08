FROM python:3.9-alpine
ENV PYTHONUNBUFFERED=1
COPY ./requirements.txt ./
RUN ls && apk add --update --no-cache postgresql-client postgresql-dev gcc libc-dev linux-headers
RUN pip install -r /requirements.txt
RUN mkdir /app 
WORKDIR /app
COPY ./app /app
RUN addgroup -S django && adduser -S django -G django
USER django 
