# 1. Expect a single, full image URL passed from Jenkins
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

# 2. Add your custom configurations
LABEL maintainer="Approved Images Team"
RUN echo "Building image using parent: ${BASE_IMAGE}"
