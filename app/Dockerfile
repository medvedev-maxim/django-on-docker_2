# pull official base image
FROM python:3.9.6-alpine

# set work directory
#WORKDIR /usr/src/app
RUN mkdir -p /home/app/web
RUN mkdir /home/app/web/static
WORKDIR /home/app/web

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install psycopg2 dependencies
RUN apk update \
    && apk add postgresql-dev gcc python3-dev musl-dev

# install dependencies
RUN pip install --upgrade pip
#COPY ./requirements.txt .
COPY requirements.txt /home/app/web
RUN pip install -r requirements.txt

# copy entrypoint.sh
#COPY ./entrypoint.sh .
COPY entrypoint.sh /home/app/web

#RUN sed -i 's/\r$//g' /usr/src/app/entrypoint.sh
#RUN chmod +x /usr/src/app/entrypoint.sh
RUN sed -i 's/\r$//g' /home/app/web/entrypoint.sh
RUN chmod +x /home/app/web/entrypoint.sh


# copy project
COPY . .

# run entrypoint.sh
ENTRYPOINT ["/home/app/web/entrypoint.sh"]
#ENTRYPOINT ["/usr/src/app/entrypoint.sh"]
