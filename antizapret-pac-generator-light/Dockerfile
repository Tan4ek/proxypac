FROM python:3.7-slim

COPY . /app

WORKDIR /app

# from config.sh
# HTTPS (TLS) proxy address
ENV PACSOCKS5HOST=exapmle.proxy:3143
ENV PACFILE=proxy-host.pac
ENV PACFILE_NOSSL=proxy-host-nossl.pac
# Perform DNS resolving to detect and filter non-existent domains
ENV RESOLVE_NXDOMAIN=yes

RUN pip install --no-cache-dir dnspython
RUN apt update && apt install -y \
   idn \
   curl \
   coreutils \
   gawk \
   sipcalc \
   cron \
    && rm -rf /var/lib/apt/lists/*

# Create the log file to be able to run tail
RUN touch /var/log/cron.log

# Setup cron job
# 0 2 * * *  - every day at 2am
RUN (crontab -l ; echo "0 2 * * * cd /app/ && ./doall.sh >> /var/log/cron.log") | crontab

# Run the command on container startup
CMD /app/doall.sh && cron && tail -f /var/log/cron.log
