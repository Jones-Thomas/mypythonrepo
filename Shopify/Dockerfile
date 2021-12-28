FROM python:3.6

EXPOSE 5002
EXPOSE 3306

ENV FLASK_ENV=development
ENV FLASK_APP=shopifyapp
#ENV FLASK_APP=run.py
WORKDIR /home/fsdev/python-docker/

COPY . /home/fsdev/python-docker/

RUN python -m pip install --upgrade pip

RUN python -m pip install -r requirements.txt

CMD ["flask", "run", "--host=0.0.0.0", "-p 5002"]


# docker image build -t python-docker .
# docker run --name shopify-flask-app --network=host -dit -p 5002:5002 shopify-flask-image
