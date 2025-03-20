FROM python:3

LABEL maintainer="rhernandez35@my.bcit.ca"

RUN mkdir -p /app
RUN apt-get update && apt-get install -y default-mysql-client sudo
# Copy just the requirements.txt first to leverage Docker cache
# on `pip install`
COPY ./requirements.txt /app/requirements.txt

# Set the working directory
WORKDIR /app
# Install dependencies
RUN pip3 install -r requirements.txt
# Copy the source code
COPY . /app

# Change permissions and become a non-privileged user
# RUN chown -R nobody:nogroup /app

# Add nobody to sudo group and grant sudo privileges
RUN usermod -aG sudo nobody && \
    echo "nobody ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER nobody

# Tells on which port the service listens in the container
EXPOSE 8090

# Entrypoint = run Python
ENTRYPOINT [ "python3" ]

# Default = run app.py
CMD [ "app.py" ]
