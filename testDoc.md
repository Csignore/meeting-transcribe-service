# docker-parrot
> a meeting transcription service

## Installation
1. Install docker and set the enviornment to Linux.
2. Pull the latest docker images
```
docker pull ychenvin/mtsparrot
```

## Run the image
1. start the server:
```
docker run -d -p 8888:3000 mtsapp
```

2. view the real-time command line logs of the container: 
``` 
docker ps
```
&
```
docker logs -f ${the running container id}
```

## Test
1. Go to [localhost:8888/enroll](localhost:8888/enroll) and follow the instructions to enroll your email address and your voice sample.
2. Use the pre-registered email address to send a meeting invitation to [wavesbot319@outlook.com](); make sure the email body contains ``` [meeting phone number: 7778889999]```*.
3. Upon this point, the logs in the terminal should have some POST request which indicates meeting created/updated/deleted.
4. If the phone number in the email body is matched with the twillio phone number, you should expect a call when it is the meeting time.
5. Once finished the phone call, MTS will start its transcription and recognize the speakers. 

Sample output in the terminal:

```
> parrot@0.0.0 start /Users/Vince/Projects/meeting-transcribe-service
> node ./bin/www

https://wet-eagle-95.localtunnel.me
Database successfully connected.
AccessToken has expired.
Requesting new AccessToken with RefreshToken...
Tokens saved.
Notification URL updated.
POST /email?validationToken=Validation%3a+Testing+client+application+reachability+for+subscription+Request-Id%3a+336960d6-2589-9366-b34e-2f45c1379c9f 200 3.240 ms - 117
Microsoft Graph API Subscription created. Id: eb305c17-c17b-4b22-a757-215d9590e12c
Current subscriptions:
[
  {
    "id": "eb305c17-c17b-4b22-a757-215d9590e12c",
    "resource": "me/events",
    "applicationId": "220cf0fd-9bf3-47fb-b86d-7976d3ffafd4",
    "changeType": "created,updated",
    "clientState": null,
    "notificationUrl": "https://wet-eagle-95.localtunnel.me/email",
    "expirationDateTime": "2019-11-17T02:21:23.975Z",
    "creatorId": "00037FFE262C380D"
  }
]
Server started. Listening on port: 3000

Database updated.
POST /email 202 1853.062 ms - 8
Calling to meeting:AQMkADAwATM3ZmYAZS0yNjJjLTM4MGQtMDACLTAwCgBGAAAD8qzntYMa0UmNcvdfBhUq0gcADCxh1Fj7O0a5Tk9J4AgFYAAAAgENAAAADCxh1Fj7O0a5Tk9J4AgFYAAAABW6qIMAAAA=
Map { 1 => [ [ 0, 7.1 ], [ 8.5, 12.6 ] ] }
Processing finished !
6e414b2e-372c-41f2-9077-2e68b3d074ab
https://cs319speechrecog.cognitiveservices.azure.com/spid/v1.0/operations/d1f76ebb-8e53-4e43-b9d0-18f2cd16df37
```

Sample output files in the /services/transcibe/output

```
{meetingID}.txt
speaker1.wav
speaker2.wav
```

* for now, the phone number can only be Vincent's phone number, because twillio trial account only allows one phone number.

## Conclusion
This is the integrated product of the meeting transcibe services. All the components are deployed in the docker image. 