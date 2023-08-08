FROM debian:11-slim AS build

# install necessary software packages and libraries using package managers like apt-get (for Debian-based images) or yum (for Red Hat-based images).
RUN apt-get update && \
    apt-get install --no-install-suggests --no-install-recommends --yes python3-venv gcc libpython3-dev && \
    python3 -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel

FROM build AS build-venv

COPY requirements.txt /requirements.txt

# install necessary software packages and libraries using package managers like apt-get (for Debian-based images) or yum (for Red Hat-based images).
RUN /venv/bin/pip install --disable-pip-version-check -r /requirements.txt

FROM gcr.io/distroless/python3-debian11

COPY --from=build-venv /venv /venv

COPY main.py .

ENTRYPOINT ["/venv/bin/python3", "main.py"]

# Define Entrypoint or Command: Define the default command to run when the container starts. This can be an executable or script that starts your application.
# CMD [ "executable" ]