FROM python:3.13.18-slim-trixie

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
   ca-certificates \
   libbrotli1 \
   idn \
   curl \
   coreutils \
   gawk \
   sipcalc \
    && dpkg --compare-versions "$(dpkg-query -W -f='${Version}' libbrotli1)" ge '1.1.0-2+deb13u1' \
    && rm -rf /var/lib/apt/lists/*

# Run the command on container startup
CMD /app/doall.sh
