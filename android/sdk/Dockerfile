FROM snowdream/gradle:3.4

MAINTAINER howard000 <howard000@gmail.com>

# Install dependencies
RUN dpkg --add-architecture i386 && \
    apt-get -qq update && \
    apt-get -qqy install libc6:i386 libstdc++6:i386 zlib1g:i386 libncurses5:i386 tar git --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# Download and untar Android SDK
ENV ANDROID_SDK_VERSION r24.4.1
ENV ANDROID_SDK_URL http://dl.google.com/android/android-sdk_${ANDROID_SDK_VERSION}-linux.tgz
RUN curl -sSL "${ANDROID_SDK_URL}" -o android-sdk_${ANDROID_SDK_VERSION}-linux.tgz \
  && tar --no-same-owner -xz -f android-sdk_${ANDROID_SDK_VERSION}-linux.tgz -C ${SDK_HOME}  \
  && rm -rf android-sdk_${ANDROID_SDK_VERSION}-linux.tgz

ENV ANDROID_HOME ${SDK_HOME}/android-sdk-linux
ENV ANDROID_SDK ${SDK_HOME}/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

# Install Android SDK components

ENV ANDROID_COMPONENTS platform-tools,build-tools-25.2.3,android-25
ENV GOOGLE_COMPONENTS extra-android-m2repository,extra-google-m2repository

RUN echo y | android update sdk --no-ui --all --filter "${ANDROID_COMPONENTS}" ; \
    echo y | android update sdk --no-ui --all --filter "${GOOGLE_COMPONENTS}"
