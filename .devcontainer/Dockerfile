FROM mcr.microsoft.com/devcontainers/rust:bookworm

RUN cargo install create-tauri-app --locked
RUN apt update && apt install nodejs npm -y
RUN apt install libwebkit2gtk-4.0-dev \
    build-essential \
    curl \
    wget \
    file \
    libssl-dev \
    libgtk-3-dev \
    libayatana-appindicator3-dev \
    librsvg2-dev -y