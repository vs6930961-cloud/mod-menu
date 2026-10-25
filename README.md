name: build
on: [push, workflow_dispatch]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: unzip -q cheatmenu-1.16.5-project.zip
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/gradle-build-action@v2
        with:
          gradle-version: 7.3.3
          arguments: build --no-daemon
          build-root-directory: cheatmenu
      - uses: actions/upload-artifact@v4
        with:
          name: cheatmenu-jar
          path: cheatmenu/build/libs/*.jar
