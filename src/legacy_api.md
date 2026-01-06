# Legacy API

<div style="background-color: rgb(61, 44, 0); border: 1px solid rgb(251, 212, 106); color: rgb(251, 212, 106); padding: 15px; border-radius: 5px; margin-bottom: 15px;">
    This API has been deprecated in favor of the <a href="./software_api.md" style="color: #3498db; text-decoration: underline;">Software API</a>.
</div>

The Legacy API is an extremely basic set of KM-style Mouse commands used to control Ferrum's functionality from
platforms that don't support the APIs provided by the Ferrum App.

For the latest features **avoid using the Legacy API unless absolutely necessary**. The only time it should be used is
if the user uses Linux for their input pc.

To connect to the Legacy API, please connect directly to the "Silicon Labs CP210x" COM port on your input pc. The
starting port speed is 115200. This speed will reset to 115200 every time the device re-powers.

The following sections provide information and pseudocode examples for the different commands available.