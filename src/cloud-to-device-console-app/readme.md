# LVA cloud to device sample console app

This directory contains a dotnet core sample app that would enable you to invoke LVA on IoT Edge Direct Methods in a sequence and with parameters, defined by you in a JSON file (operations.json)

## Contents

| File/folder             | Description                                                   |
|-------------------------|---------------------------------------------------------------|
| `.gitignore`            | Define what to ignore at commit time.                         |
| `README.md`             | This README file.                                             |
| `operations.json`       | JSON file defining the sequence of operations to execute upon.|
| `main.py`               | The main program file                                         |
| `requirements.txt`      | List of all dependent Python libraries                        |


## Setup

Create a file named `appsettings.json` in this folder. Add the following text and provide values for all parameters.

```JSON
{
    "IoThubConnectionString" : "<your iothub connection string>",
    "deviceId" : "<device ID>",
    "moduleId" : "<module ID>"
}
```

* **IoThubConnectionString** - Refers to the connection string of your IoT hub. This should have registry write and service connect access.
* **deviceId** - Refers to your IoT Edge device ID (registered with your IoT hub)
* **moduleId** - Refers to the module ID of LVA on IoT Edge module (when deployed to the IoT Edge device).

> [!TIP]
> Running [LVA resources setup script](https://github.com/Azure/live-video-analytics/tree/master/edge/setup), generates **appsettings.json** file with values pre-filled by the script.

Create a file named `.env` in the `src/edge` folder and add the following text to it. Provide values for all variables.

```env
CONTAINER_REGISTRY_USERNAME_myacr=""
CONTAINER_REGISTRY_PASSWORD_myacr=""
SUBSCRIPTION_ID=""
RESOURCE_GROUP=""
AMS_ACCOUNT=""
AAD_TENANT_ID=""
AAD_SERVICE_PRINCIPAL_ID=""
AAD_SERVICE_PRINCIPAL_SECRET=""
VIDEO_OUTPUT_FOLDER_ON_DEVICE=""
VIDEO_INPUT_FOLDER_ON_DEVICE=""
APPDATA_FOLDER_ON_DEVICE=""
```

> [!TIP]
> Running [LVA resources setup script](https://github.com/Azure/live-video-analytics/tree/master/edge/setup) generates the `.env` file with values pre-filled by the script.

## Running the sample from Visual Studio Code

Detailed instructions for running the sample can be found in the tutorials for LVA on IoT Edge. Below is a summary of key steps. Make sure you have installed the required [prerequisites](./../../README.md#prerequisites).

* Right click on src/edge/deployment.template.json and select **“Generate Iot Edge deployment manifest”**. This will create an IoT Edge deployment manifest file in src/edge/config folder named deployment.amd64.json.
* Right click on src/edge/config /deployment.amd64.json and select **"Create Deployment for single device"** and select the name of your edge device. This will trigger the deployment of the IoT Edge modules to your Edge device. You can view the status of the deployment in the Azure IoT Hub extension (expand 'Devices' and then 'Modules' under your IoT Edge device).
* Right click on your edge device in Azure IoT Hub extension and select **"Start Monitoring Built-in Event Endpoint"**.
* Install python dependencies from `requirements.txt`. This can be done by running `pip install -r src\cloud-to-device-console-app\requirements.txt`.
* Select the "Cloud to Device - Console App" configuration in the run tab and start a debugging session (hit F5). You will start seeing some messages printed in the TERMINAL window. In the OUTPUT window, you will see messages that are being sent to the IoT Hub, by the lvaEdge module.

## Troubleshooting

See the [Live Video Analytics Troubleshooting page](https://docs.microsoft.com/en-us/azure/media-services/live-video-analytics-edge/troubleshoot-how-to).

## Next steps

Experiment with different sequence of Direct Method calls by modifying operations.json.
