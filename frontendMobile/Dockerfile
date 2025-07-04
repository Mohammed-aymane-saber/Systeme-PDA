FROM node:18-bullseye

ENV ANDROID_HOME=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools

# Installer dépendances système indispensables
RUN apt-get update && apt-get install -y \
    openjdk-11-jdk wget unzip git curl libgl1-mesa-glx libpulse0 \
  && rm -rf /var/lib/apt/lists/*

# Installer yarn si besoin
RUN if ! command -v yarn > /dev/null; then npm install -g yarn; else echo "Yarn already installed"; fi

# Installer Android command line tools
RUN mkdir -p $ANDROID_HOME/cmdline-tools && \
    cd $ANDROID_HOME && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip -O tools.zip && \
    unzip tools.zip -d cmdline-tools_temp && \
    mv cmdline-tools_temp/cmdline-tools $ANDROID_HOME/cmdline-tools/latest && \
    rm -rf cmdline-tools_temp tools.zip

# Installer platform-tools Android SDK
RUN wget https://dl.google.com/android/repository/platform-tools_r33.0.3-linux.zip -O platform-tools.zip && \
    unzip platform-tools.zip -d $ANDROID_HOME && \
    rm platform-tools.zip

WORKDIR /app

COPY . .

RUN yarn install

EXPOSE 8081

CMD ["yarn", "start"]
