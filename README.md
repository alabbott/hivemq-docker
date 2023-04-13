# HiveMQ MQTT Broker with Docker Compose

This repository contains a `docker-compose.yaml` file that allows you to easily set up and run a HiveMQ MQTT broker with Docker Compose. HiveMQ is an MQTT broker designed for enterprises and is built for reliability and scalability. MQTT (Message Queuing Telemetry Transport) is a lightweight messaging protocol that provides resource-constrained network clients with a simple way to distribute telemetry information.

## Prerequisites

Before you can use the provided `docker-compose.yaml` file, you need to have Git, Docker, and Docker Compose installed on your system. If you don't already have them installed, follow these instructions to install Git, Docker, and Docker Compose:

### Windows

1. Download and install [Git for Windows](https://git-scm.com/download/win).
2. Download and install [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop).
3. After the installation is complete, Docker should start automatically. If it doesn't, you can start it manually by running "Docker Desktop" from the Start menu.
4. Docker Compose is included with Docker Desktop for Windows, so you don't need to install it separately.

### Linux

1. Follow the instructions to install [Git](https://git-scm.com/download/linux) for your specific Linux distribution.
2. Follow the instructions to install [Docker Engine](https://docs.docker.com/engine/install/) for your specific Linux distribution.
3. Install Docker Compose using the [official installation guide](https://docs.docker.com/compose/install/).

## Getting Started

Follow these steps to get the HiveMQ MQTT broker up and running:

1. Open a terminal (Command Prompt on Windows, Terminal on Linux) and navigate to the directory where you want to store the project files.
2. Clone this repository:

        git clone https://github.com/alabbott/hivemq-docker.git


3. Change to the newly created directory:

        cd hivemq-docker

4. Run the `docker-compose.yaml` file:

        docker-compose up -d

    Note you may have to use sudo if on Linux

        sudo docker-compose up -d


5. The HiveMQ MQTT broker should now be running, and you can access the control center by navigating to `http://localhost:8080` in your web browser.

    Default Control Center credentials:

    - User: admin
    - Password: hivemq

## Testing the Server with MQTTX Client

To test the MQTT server, you can use the MQTTX client, a cross-platform MQTT desktop client with a user-friendly interface.

1. Download and install [MQTTX](https://mqttx.app/) for your platform (Windows, macOS, or Linux).
2. Open MQTTX and click "New Connection."
3. Enter the following details:
- Name: `HiveMQ Test`
- Host: `localhost`
- Port: `1883`
- Username: `admin-user`
- Password: `admin-pass`
4. Click "Save" and then "Connect."
5. You should now be connected to your HiveMQ MQTT broker. You can publish and subscribe to topics to test the functionality.

There is another user created by default with reduced permissions:
- Username: user1
- Password: pass1

## Exposing the MQTT Server on the Internet

To make the MQTT server available on the internet, you can use Azure Networking rules. Follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Create a new Virtual Machine or navigate to an existing one.
3. In the left-hand menu, click on "Networking."
4. Click "Add inbound port rule."
5. Add a new rule for the MQTT port (1883) and Control Center port (8080), with the following settings:

   - Source: Any
   - Source port ranges: *
   - Destination: Any
   - Destination port ranges: 1883, 8080
   - Protocol: TCP
   - Action: Allow
   - Priority: Choose a unique priority number
   - Name: MQTT and Control Center

6. Click "Add" to create the rule.

After completing these steps, your MQTT server should be accessible from the internet. Please note that exposing your server to the internet can lead to security risks. Ensure that you have proper authentication and encryption in place before doing so.
