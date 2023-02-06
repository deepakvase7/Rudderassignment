# Rudderassignment


This repository contains 3 files

1. javascript_page.html
2. rudder-docker.yml
3. postman-collection-import

1-> It contains the Javascript and HTML code for our application.In this we have also added the script for integrating with Rudderstack.

2->This file contains configuration for running the app on local Docker environment.

3->This is the postman collection which is imported in Postman app and then used for sending & testing for various events like 'track','page',etc.



******** Step 1 ******** 
Rudderstack app setup 

To open the rudderstack application .Follow the steps given below :

1.Go to rudderstack.com -> Login
2.Login using email id 'lioneltendulkar7@gmail.com' and password 'Mrspass@123456'

Here you could see source , destination and transformation

Source used is Javascript .
Destination is a webhook where you can check incoming data . (https://webhook.site/801cda44-4128-467e-8c07-139d39ac850f)
In transformation we can filter event ,clean data etc.  


******** Step 2 ********
Created a simple JS website  and sent events to rudderstack

Open javascript_page.html in a browser to open the website.

It consists 'Add to cart' and 'Checkout button' which trigger the track events.

After clicking on any of the buttons alert is displayed informing the user that button was clicked .
Enter OK.
To check if events are reaching to the destination .Go to the webhook url https://webhook.site/801cda44-4128-467e-8c07-139d39ac850f 

******** Step 3 ********
Moved to developer setup / docker

Then I sent the data through a local Docker setup by installing Rudderstack on a local directory by using rudder-docker.yml file .

 From terminal ,Generated events using command - 'docker exec -ti \
    6fa3db359461 \
    ./scripts/generate-event 2LF0VGOyiFJsY1VZ9EfOH27Lyw2 https://gmaillionynmy.dataplane.rudderstack.com/v1/batch'

And later checked the events  on the destination(webhook) if the event was coming or not. Events were showing up successfully on the webhook.

******** Step 4 ********
Created a user transformation to drop/filter the events

Using the below transformEvent function dropped the event if the event is of type 'identify' and filtered/chagned the OS context to Ubuntu if event is of type 'page'

_export function transformEvent(event) {
    
    
    if (event.type==='identify') return ;   //droping the event if event type is identify
    
        if (event.type==='page')
        event.context.os = { name: "Ubuntu"};  //changing context os to Ubuntu
        return event;
        
        
        
    
    return event;
}_


Also imported the postman collection and tested events from Postman.

Thanks,
Deepak Survase
