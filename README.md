# GitHub-Discord-HookRouter
All your webhooks with one URL.
A Lightweight API that routes github webhook requests to Discord. Allows easy management of multiple webhooks. Features signature verification, rate-limit handling, IP banning and verification, and cool logging.

This API allows you to send requests to multiple Discord webhooks which is sent from GitHub. As you guessed it, this API will act as the POSTman in delivering the requests. This API also auto-bans IP addresses on repeated access if it is unauthorized.

**Precautions**:
1) Use only one webhook URL on all your repository (which should be the link to reach this API).
2) It is highly recommended to protect this endpoint with signature verification to prevent unauthorized access to your API. More info about creating a secure secret with a high entropy could be found [here](https://developer.github.com/webhooks/securing/).
3) This API also supports SSL verification header sent by GitHub.
4) The content type should be set to `application/json` when the GitHub webhook is being created, or it will cause unintended issues as Discord can't parse any other content-type.
5) Although this API supports handling requests from the baseURL, we recommend you to use the allocated path of the webhook. For example, use the path `/github` if you're using this API for managing GitHub requests.

## Instructions on setting it up!
1) Copy paste the [config.template.json](https://github.com/Khaazz/GitHub-Discord-HookRouter/template/config-template.json) in [configs/config.json](https://github.com/Khaazz/GitHub-Discord-HookRouter/configs/).
```js
{
    "port": "3000",
    "auth": true,
    "authorization": "Secret key",
    "blacklisted": []
}
```

2) If you want to secure your API using the github webhook secret, set `auth` to ̀`true` and set the property of `authorization` as the secret key.

3) You can manually blacklist IP addresses by adding those to the `blacklisted` property. The API will automatically refuse connections from those IP addresses.

4) Copy paste the [webhooks.template.json](https://github.com/Khaazz/GitHub-Discord-HookRouter/template/webhooks-template.json) in [configs/webhooks.json](https://github.com/Khaazz/GitHub-Discord-HookRouter/configs/).
```js
[
    {
        "name": "webhook",
        "id": "webhookID",
        "token": "webhookToken"
    }
]
```
The webhooks config contains the array of all webhooks you want to manage.
Provide a name, webhook's id, and token and you are good to go.

5) When setting up the webhook in github, copy the url to access this API with the path as `/github`. Don't forget to change the content type to `application/json` and provide a secret token if you are going to use one. Same goes for setting up GitLab webhooks.

6) Start this API by executing `node src/app.js` in the console. [PM2 script](https://github.com/Khaazz/GitHub-Discord-HookRouter/scripts/start.js) is located in the scripts folder which could be used if you want to use PM2.
Alternatively, you can use `npm start` or `npm pm2start`.

7) If you want to quickly host this API, you could use ngrok; which is available [here](https://ngrok.com/).

## Contributions
Feel free to contribute to this project by opening Pull-Request or Issues.
Contributions are always welcome.

## Honorable mentions
Huge thanks to [Santhosh-Annamalai](https://github.com/Santhosh-Annamalai) for being helpful when building this API.
