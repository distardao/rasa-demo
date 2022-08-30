<div id="top"></div>
<!--
*** Thanks for checking out the rasa-demo. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![GNU V3 License][license-shield]][license-url]
<!-- [![LinkedIn][linkedin-shield]][linkedin-url] -->


<!-- PROJECT LOGO -->
<br />
<div align="center">
    <a href="https://github.com/distardao/rasa-demo">
        <img src="images/logo.png" alt="Logo" width="80" height="80">
    </a>

  <h3 align="center">Sara</h3>

  <p align="center">
    The document describes in detail how to install and use sara bot 
    <br />
    <a href="https://github.com/distardao/rasa-demo"><strong>Document details »</strong></a>
    <br />
    <br />
    <!-- <a href="https://github.com/distardao/rasa-demo">View Demo</a>
    · -->
    <a href="https://github.com/distardao/rasa-demo/issues">Bugs report</a>
    ·
    <a href="https://github.com/distardao/rasa-demo/issues">Feature request</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details open="true">
    <summary>Table of contents</summary>
    <ul>
        <li>
            <a href="#introduction">Introduction</a>
            <ul>
                <li><a href="#technology">Technology</a></li>
            </ul>
        </li>
        <li>
            <a href="#getting-started">Getting started</a>
            <ul>
                <li><a href="#requirements">Requirements</a></li>
                <li><a href="#installation">Installation</a></li>
                <li><a href="#project-structure">Project Structure</a></li>
            </ul>
        </li>
        <li>
            <a href="#usage">Usage</a>
            <ul>
                <li>
                    <a href="#training">Training</a>
                    <ul>
                        <li><a href="#train-models-from-source
">Train models from source</a></li>
                        <li><a href="#train-models-from-docker">Train models from docker</a></li>
                    </ul>
                </li>
                <li>
                    <a href="#run-the-whole-system">Run the whole system</a>
                    <ul>
                        <li><a href="#run-from-repo">Run from source</a></li>
                        <li><a href="#run-from-docker">Run from docker</a></li>
                    </ul>
                </li>
            </ul>
        </li>
        <!-- <li><a href="#roadmap">Roadmap</a></li> -->
        <li><a href="#contributing">Contributing</a></li>
        <li><a href="#license">License</a></li>
        <li><a href="#contact">Contact</a></li>
        <!-- <li><a href="#acknowledgments">Acknowledgments</a></li> -->
    </ul>
</details>


<br/>

<!-- ABOUT THE PROJECT -->
## Introduction

<!-- <br/> -->

<!-- <img src="images/home_screenshot.png" alt="home_screenshot"> -->

<!-- <br/> -->
<!-- <br/> -->

The purpose of this repo is to showcase a contextual AI assistant built with the open source Rasa framework.

Sara is an alpha version and lives in our docs, 
helping developers getting started with our open source tools. It supports the following user goals:

- Understanding the Rasa framework
- Getting started with Rasa
- Answering some FAQs around Rasa
- Directing technical questions to specific documentation
- Subscribing to the Rasa newsletter
- Requesting a call with Rasa's sales team
- Handling basic chitchat

<p align="right">(<a href="#top">Back to top</a>)</p>

### Technology

This bot is built on following technologies: 

*   [Python](https://www.python.org/)
*   [Docker](https://www.docker.com/)
*   [Virtualenv](https://virtualenv.pypa.io/en/latest/)
*   [Rasa](https://rasa.com/)
*   [Ngrok](https://ngrok.com/)

<p align="right">(<a href="#top">Back to top</a>)</p>


<!-- GETTING STARTED -->
## Getting started

### Requirements

Before you start, make sure your environment meet following requirements:
- Python (>= 3.8.10 - tested)
- Docker (>= 20.10.17 - tested)
- Virtualenv, for development process (>= 20.13.1 - tested)
- Ngrok (>= 3.0.0 - tested)

Here are steps for setup:
* Install [Python](https://docs.python-guide.org/starting/install3/linux/) 
* Install Virtualenv

    ```sh
    sudo apt install python3-pip # if you don't have pip
    ```
    ```sh
    sudo apt install virtualenv
    ```
* Install [Docker engine](https://docs.docker.com/engine/install/ubuntu/)
* Install ngrok
    ```sh
    snap install ngrok
    ```
    ```sh
    ngrok config add-authtoken <token> # You can get this token from your ngrok account https://dashboard.ngrok.com/get-started/setup
    ```

<p align="right">(<a href="#top">Back to top</a>)</p>

### Installation
#### Install from repo

1.  Clone this repo

    ```sh
    git clone https://github.com/your_username_/rasa-demo # you can clone from your forked repo or main repo
    ```
2.  Navigate to the main directory
3.  Create new virtual environment (Inside project directory) 

    ```sh
    virtualenv ./.venv # The name of virtual environment should be ".venv" to prevent pushing this directory to git server
    ```
    ```sh
    source .venv/bin/activate # Activate this environment
    ```
4.  Install all required packages
    ```sh
    pip install -r requirements.txt
    ```
5. Create new "credentials.yml" file and add following data:
    ```yml
    telegram:
      access_token: "<your telegram bot access token>"
      verify: "<your telegram bot name>"
      webhook_url: "<ngrok url>/webhooks/telegram/webhook" # You can get this url after running ngrok service, example: https://702c-85-203-21-21.ap.ngrok.io
    ```

<p align="right">(<a href="#top">Back to top</a>)</p>

#### Install from docker

1. Create new network 

    ```sh
    sudo docker network create rasa-bot-demo
    ```
2. Create new "credentials.yml" file and add following data:
    ```yml
    telegram:
      access_token: "<your telegram bot access token>"
      verify: "<your telegram bot name>"
      webhook_url: "<ngrok url>/webhooks/telegram/webhook" # You can get this url after running ngrok service, example: https://702c-85-203-21-21.ap.ngrok.io
    ```
2. Build rasa action server image:

    ```sh
    sudo docker build -t rasa-demo-action-server -f Dockerfile.rasaaction .
    ```

<p align="right">(<a href="#top">Back to top</a>)</p>

### Project structure 

This project contains main files and directories:
* actions: Folder containing logic of actions, you can define various reactions such as calling api, querying and returning data from database, ... 
* config.yml: This file defines the components and policies that your model will use to make predictions based on user input.
* domain.yml: This file specifies the intents, entities, slots, responses, forms, and actions your bot should know about. It also defines a configuration for conversation sessions.
* credentials.yml: This file define necessary credentials used when interacting with external system.
* endpoints.yml: This file define all endpoints that the main server shoud know, such as action server, ...
* Dockerfile.rasaaction: The docker file defines the environment that action server run from. 


<!-- USAGE EXAMPLES -->
## Usage

### Training
#### Train models from source 
<strong>(*)</strong> At first, you need to activate your virtual environment
```sh
virtualenv ./.venv
```

For training, run this command:
```sh
rasa train
```
<p align="right">(<a href="#top">Back to top</a>)</p>

#### Train models from docker

To train models, run this command:
```sh
sudo docker run -v $(pwd):/app rasa/rasa:3.2.0-full train --domain domain.yml --data data --out models
```

<strong>(*)</strong> If you want to train models faster, try the training command with
`--augmentation 0`), the training process will ignore augmentation step.

<p align="right">(<a href="#top">Back to top</a>)</p>

### Run the whole system
#### Run from source
1. Open new terminal, navigate to this project directory and activate virtual environment
2. Run this command for the main server:

    ```sh
    rasa run
    ```
3. Open another terminal, also in the current directory, run this command for rasa action server:

    ```sh
    rasa run actions --actions actions.actions
    ```
4. Open the third terminal, run duckling service:
    ```sh
    sudo docker run -p 8000:8000 rasa/duckling
    ```
5. Run ngrok:
    ```sh
    ngrok http 5005
    ```

<p align="right">(<a href="#top">Back to top</a>)</p>

#### Run from docker
1. Run main server by following command:

    ```sh
    sudo docker run --name=rasa-demo-server --net=rasa-bot-demo -p 5005:5005 -v $(pwd):/app rasa/rasa:3.2.0-full run
    ```
2. Run action server by following command:

    ```sh
    sudo docker run --name=rasa-demo-action-server --net=rasa-bot-demo -p 5055:5055 rasa-action-server
    ```
3. Run duckling service:

    ```sh
    sudo docker run --name=rasa-demo-duckling --net=rasa-bot-demo -p 8000:8000 rasa/duckling
    ```
4. Run ngrok serivce:

    ```sh
    sudo docker run --net=rasa-bot-demo -it -e NGROK_AUTHTOKEN=<token> ngrok/ngrok:alpine http rasa-demo-server:5005 # Get this token from your ngrok account
    ```

<p align="right">(<a href="#top">Back to top</a>)</p>

<!-- CONTRIBUTING -->
## Contributing
If you want to contribute to this project, please do following steps:
1. Fork this project
2. Write your code and push them to your fork
3. Create a merge request to the main project (main branch)
4. Tag this account "distardao" in your merge request comment box

We all wellcome your fantastic ideas  

<p align="right">(<a href="#top">Back to top</a>)</p>

<!-- LICENSE -->
## License

Distributed under the GNU GENERAL PUBLIC LICENSE V3. See `LICENSE` for more information.

<!-- Distributed under the MIT License. See `LICENSE.txt` for more information. -->

<p align="right">(<a href="#top">Back to top</a>)</p>



<!-- CONTACT -->
## Contact

TODO

<!-- Your Name - [@your_twitter](https://twitter.com/your_username) - email@example.com
Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name) -->

<p align="right">(<a href="#top">Back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/distardao/rasa-demo.svg?style=for-the-badge
[contributors-url]: https://github.com/distardao/rasa-demo/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/distardao/rasa-demo.svg?style=for-the-badge
[forks-url]: https://github.com/distardao/rasa-demo/network/members
[stars-shield]: https://img.shields.io/github/stars/distardao/rasa-demo.svg?style=for-the-badge
[stars-url]: https://github.com/distardao/rasa-demo/
[issues-shield]: https://img.shields.io/github/issues/distardao/rasa-demo.svg?style=for-the-badge
[issues-url]: https://github.com/distardao/rasa-demo/issues
[license-shield]: https://img.shields.io/github/license/distardao/rasa-demo.svg?style=for-the-badge
[license-url]: https://github.com/distardao/rasa-demo/blob/main/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/distardao
[product-screenshot]: images/screenshot.png