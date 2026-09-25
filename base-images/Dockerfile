# 1. Declare the argument name
ARG BASE_FLAVOR

# 2. Use the exact Red Hat registry URL and include the '$' before the braces
FROM ://redhat.com{BASE_FLAVOR}

# Add your custom layers below
LABEL maintainer="Approved Images Team"
RUN echo "Successfully building from base flavor: ${BASE_FLAVOR}"
