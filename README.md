# DHBW WebEngineering Projekt - Ilja Kalistratov

Web Engineering Project for the DHBW Stuttgart (3.Semester). 

This PWA ("Progressive Web App") is kind of an information service initially for cities and villages. But also countries do work.

The information consists of:
- current weather data
- summed up information/article about your search query (wikipedia)

This application does not have a backend. That means that, everything is computed in the frontend.

## Project setup
1. get your api key on https://openweathermap.org/api
2. clone this repo
3. put your api key into .env
4. cd to the project folder
5. run `npm install` to install the dependencies

Now the application should be installed properly

### Compiles and hot-reloads for development
To start the application please run the command `npm run serve`.

Note: This starts/serves the application in dev-mode. That means that warnings in the browser console may occure.


## Features
- Search for City or Country
- Shows current relevant weather data
- conditional background:
(warm weather -> summer background, cold weather -> winter background, day & night background)
- Shows the first paragraph (summary) of the matching wikipedia article
- Option to let your browser read the summary (Speech Synthesis)

## Secrets & Keys
This project requires an API-Key for the OpenWeatherMap-API.
It is essential to type or copy it to the .env file. Without it this application will not work properly.

## Known Isssues (working on fixes)
- You may need to press Enter multiple times (2 - 4), to load the article properly
- Hard Coded API-Key, because of Problems of dotenv with Vue


## Used Libraries & Technologies
VUE 3 - https://vuejs.org/

https://openweathermap.org/api

https://github.com/spencermountain/wtf_wikipedia

https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API

