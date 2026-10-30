
name: Compilar FLAMENGO APK

on:
  workflow_dispatch:

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Obter ficheiros
        uses: actions/checkout@v4

      - name: Extrair projeto
        run: unzip FLAMENGO_Android_Com_Gerador_APK.zip -d projeto

      - name: Preparar Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Preparar Android SDK
        uses: android-actions/setup-android@v3

      - name: Instalar ferramentas
        run: |
          sdkmanager "platform-tools" "platforms;android-35" "build-tools;35.0.0"

      - name: Preparar Gradle
        uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.9'

      - name: Compilar APK
        working-directory: projeto
        run: gradle --no-daemon assembleDebug

      - name: Guardar APK
        uses: actions/upload-artifact@v4
        with:
          name: FLAMENGO-APK
          path: projeto/app/build/outputs/apk/debug/app-debug.apk
          if-no-files-found: error
          retention-days: 7
