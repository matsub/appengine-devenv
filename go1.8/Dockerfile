FROM golang:1.8-alpine
ARG CLOUD_SDK_VERSION=218.0.0
ENV CLOUD_SDK_VERSION=$CLOUD_SDK_VERSION

WORKDIR /

ENV PATH /google-cloud-sdk/bin:$PATH
RUN apk --no-cache add \
        curl \
        python \
        py-crcmod \
        bash \
        libc6-compat \
        openssh-client \
        git \
        gnupg \
    && curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    tar xzf google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    rm google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    ln -s /lib /lib64 && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud config set metrics/environment github_docker_image && \
    gcloud components install app-engine-go && \
    gcloud components remove bq gsutil && \
    gcloud --version

RUN rm -r \
        /google-cloud-sdk/RELEASE_NOTES \
        /google-cloud-sdk/README \
        /google-cloud-sdk/VERSION \
        /google-cloud-sdk/*.inc \
        /google-cloud-sdk/deb \
        /google-cloud-sdk/rpm \
        /google-cloud-sdk/platform/ext-runtime \
        /google-cloud-sdk/.install/.download \
        /google-cloud-sdk/.install/.backup \
    && find /google-cloud-sdk/ -name "*.pyc" -delete

VOLUME ["/root/.config"]
