FROM ubuntu
# RUN apt update 2>/dev/null | grep packages | cut -d '.' -f 1
RUN echo $(date)
RUN timedatectl set-local-rtc 1
RUN apt update -y
RUN apt install -y tzdata
RUN echo 'Asia/Kolkata' > /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN apt update -y && apt upgrade -y
RUN apt install ntp -y
# RUN cd /etc/apt && ls -al && sed -i 's/in\./us\./g' sources.list
 
RUN apt update 
RUN apt install python3-dev libpq-dev nginx -y
RUN pip install django gunicorn psycopg2
ADD . /app
WORKDIR /app
EXPOSE 8000
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangokubernetesproject.wsgi"]
