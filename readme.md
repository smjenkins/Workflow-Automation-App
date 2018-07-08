Workflow Automation with Twilio - Laravel, JS,

A demo app of a rental company that allow clients to books and pay for rental stays via SMS. 
Here's how it'll work:

A host creates a vacation property listing
A guest requests a reservation for a property
The host receives an SMS notifying them of the reservation request. The host can either Accept or Reject the reservation
The guest is notified whether a request was rejected or accepted

Required Tech:
-Laravel
-PostgreSQL as the persistence layer (download if not on your device)
-ngrok (set up account if do not have one)
-Twilio phone service (start demo account)


Required Know-how: 
 - REST API knowledge.
 


## Run the application

1. download/clone and `cd` into it.

2. Install the dependencies
   $ composer install
  
3. Create a database (using PostgreSQL)
  $ createdb airtng

4. Copy the sample configuration file and edit it to match your configuration.
   $ cp .env.example .env

5. Generate an `APP_KEY`.
   $ php artisan key:generate

6. Run the migrations(charging up the database).
  $ php artisan migrate

7. Load the seed data(filling the database with dummy info).
  $ php artisan db:seed

At this point, the laravel app is up and running.  But not functional.  Still...enter "$ php artisan serve"  If all is well, you should click here "https://localhost:8000" and see no errors.  Now comes the functionality.
  --------------------------------------------------------------------------------
  Go to https://www.twilio.com/user/account/  and start a demo account.  If you have a paid account, you can skip this part. 
  Once you have your demo account, you will be assigned a number.  Set the number to send and receive sms. 
  
  You can find your `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN` under
  your
  [Twilio Account Settings](https://www.twilio.com/user/account/settings).
  You can buy a Twilio phone number here [Twilio numbers](https://www.twilio.com/user/account/phone-numbers/search)
  `TWILIO_NUMBER` should be set according to the phone number you purchased above.

  Once you have completed those steps go back to your terminal screen

8. Expose the application to the wider Internet using [ngrok](https://ngrok.com/)
   $ ngrok http 8000
   

9. Configure Twilio to call your webhooks.

 You will also need to configure Twilio to send requests to your application
 when sms are received.

 You will need to provision at least one Twilio number with sms capabilities
 so the application's users can make property reservations. You can buy a number [right
 here](https://www.twilio.com/user/account/phone-numbers/search). Once you have
 a number you need to configure it to work with your application. Open
 [the number management page](https://www.twilio.com/user/account/phone-numbers/incoming)
 and open a number's configuration by clicking on it.

 Remember that the number where you change the sms webhooks must be the same one you set on
 the `TWILIO_NUMBER` environment variable.

 ![Configure Voice](http://howtodocs.s3.amazonaws.com/twilio-number-config-all-med.gif)

 For this application, you must set the voice webhook of your number so that it
 looks something like this:

 ```
 http://<your-ngrok-subdomain>.ngrok.io/reservation/incoming
 ```

 And in this case set the `POST` method on the configuration for this webhook.

1. Run the application using Artisan.
  $ php artisan serve



## Dependencies

This application uses this Twilio helper library:
* [twilio-php](https://github.com/twilio/twilio-php)



Troubleshooting: 

localhost:8000 not showing up: the most common scenario is that your app will be reachable through address
  `http://127.0.0.1:8000`. This is important because ngrok creates the
  tunnel using only that address. So, if `http://127.0.0.1:8000` is not reachable
  in your local machine when you run the app, you must tell artisan to use this
  address. Here's how to set that up:
  $ php artisan serve --host=127.0.0.1

