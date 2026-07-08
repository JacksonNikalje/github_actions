name: Deploy Java App

on:
  push:
    branches:
      - main

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

    - name: Checkout Code
      uses: actions/checkout@v4

    - name: Setup Java
      uses: actions/setup-java@v4
      with:
        distribution: temurin
        java-version: '17'

    - name: Build Project
      run: mvn clean package

    - name: Upload Artifact
      uses: actions/upload-artifact@v4
      with:
        name: app
        path: target/*.jar

  deploy:

    needs: build

    runs-on: ubuntu-latest

    steps:

    - uses: actions/download-artifact@v4
      with:
        name: app

    - name: Azure Login
      uses: azure/login@v2
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}

    - name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v3
      with:
        app-name: mywebappdemo
        package: "*.jar"
