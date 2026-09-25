# 1. Define the argument BEFORE the FROM directive so it is accessible globally
ARG BASE_FLAVOR

# 2. Pull from Red Hat's official UBI registry dynamically
FROM ://redhat.com{BASE_FLAVOR}

# 3. Add your standard corporate setups or layers here
LABEL maintainer="Your Team Name"
RUN echo "Building flavor: ${BASE_FLAVOR}"

# ... rest of your build commands ...
