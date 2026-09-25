# Define the build argument before the FROM statement
ARG BASE_FLAVOR=ubi9-standard

# Use the dynamic argument to fetch the base image from Red Hat
FROM ://redhat.com{BASE_FLAVOR}

# Add your custom labels or configuration layers below
LABEL maintainer="Approved Images Team"
RUN echo "Successfully building from base flavor: ${BASE_FLAVOR}"
