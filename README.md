# jazmynename: Fortify on Demand Scan

# TODO: Customize trigger events based on your DevSecOps processes and typical FoD SAST scan time
on:
  workflow_dispatch:
  push:
    branches: [ "master" ]
  schedule:
    - cron: '39 19 * * 6'

jobs:
  FoD-SAST-Scan:
    # Use the appropriate runner for building your source code.
    # TODO: Use a Windows runner for .NET projects that use msbuild. Additional changes to RUN commands will be required to switch to Windows syntax.
    runs-on: ubuntu-latest
    permissions:
      actions: read
      contents: read
      security-events: write

    steps:
      # Check out source code
      - name: Check Out Source Code
        uses: actions/checkout@v3

      # Java is required to run the various Fortify utilities.
      # When scanning a Java application, please use the appropriate Java version for building your application.
      - name: Setup Java
        uses: actions/setup-java@v3
        with:
          java-version: 8
          distribution: 'temurin'
          
