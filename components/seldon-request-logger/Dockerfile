FROM registry.access.redhat.com/ubi8/python-36
LABEL name="Seldon Request Logger" \
      vendor="Seldon Technologies" \
      version="1.3.0-dev" \
      release="1" \
      summary="The payload logger for Seldon Core" \
      description="The Seldon Payload Logger allows request and response payloads from a Seldon Core inference graph to be processed and sent to an ELK endpoint"

COPY app app
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
RUN pip install gunicorn

# Add licences
RUN pip install pip-licenses
RUN mkdir ./licenses && pip-licenses --from=mixed --format=csv --output-file=./licenses/license_info.csv && \
    pip-licenses --from=mixed --format=plain-vertical --with-license-file --no-license-path --output-file=./licenses/license.txt
USER root
RUN mv ./licenses /licenses
USER default

EXPOSE 8080
ENTRYPOINT ["python"]
CMD ["app/default_logger.py"]