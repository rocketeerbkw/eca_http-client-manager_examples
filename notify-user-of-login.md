> As an administrator, I want to be notified by SMS when anyone logs into my 
> account, so that I can react to potential security breaches

1.  You'll need to add this basic twilio http client config, either in a custom
    module or just put it temporarily into `http_client_manager`:

    `twilio_http_client.http_services_api.yml`:

        Twilio:
          title: "Twilio"
          api_path: "src/api/twilio.yml"
          config:
            base_uri: "https://api.twilio.com/2010-04-01/"
            auth: ['ACCOUNT-SID', 'API-TOKEN', 'Basic']

    `src/api/twilio.yml`:

        name: "Twilio"
        apiVersion: "2010-04-01"
        description: "Twilio"
        operations:
          SendSMS:
            httpMethod: POST
            uri: Accounts/{AccountSid}/Messages.json
            summary: Send SMS
            parameters:
              AccountSid:
                type: string
                location: uri
                description: Twilio Account SID
                required: true
              MessagingServiceSid:
                type: string
                location: formParam
                description: Twilio Messaging Service SID
                required: true
              To:
                type: string
                location: formParam
                description: Phone number
                required: true
              Body:
                type: string
                location: formParam
                description: SMS Body
                required: true
            responseModel: Message

        models:
          Message:
            type: object
            properties:
              body:
                location: json
                type: string
              from:
                location: json
                type: string
              to:
                location: json
                type: string
              status:
                location: json
                type: string
              error_code:
                location: json
                type: string
              error_message:
                location: json
                type: string

2.  Import the ECA model `notify_admin_of_login-0.1.1-bpmn_io-process_lvidlcb.tar.gz`
3.  You can view the model by going to `admin/config/workflow/eca/process_lvidlcb/edit`
    in your Drupal site

If you want to actually run this model, you'll need to do the following:

1.  Create a [Twilio][1] account
2.  Update the `twilio_http_client.http_services_api.yml` file with your Twilio
    credentials
3.  Import a simple Drupal configuration called `twilio_http_client.settings`
    with the following format:

        account_sid: "Your Account SID"
        messaging_sid: "Your Messaging SID"


[1]: https://twilio.com/
