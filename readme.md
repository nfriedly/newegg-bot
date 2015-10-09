Verizon "Smart Rewards" Bot
===============================

Logs into your Verizon account and visits the smart rewards page. This:

* Automatically grants you 300 points for logging in (once per billing cycle)
* Automatically grants you a free entry for the current Samsung Tablet sweepstakes (once per day)

It can optionally send out an email with the screenshots and logs always or just on errors.

Finally, the app has (commented out) code to spend more points entering the tablet sweepstakes which can be easily 
enabled and/or enhanced.

Also check out my [analysis of what the points are worth in gift card auctions](https://gist.github.com/nfriedly/b80b569e2be2d2c86c18).


Installation
------------

Requires node.js >= 4.x, then from the directory with the code run `npm install`.

Usage
-----

First create a file named `.env` and add the following:

```

# optional - send yourself an email with the results
EMAIL=<your email address>
SENDGRID_USERNAME=<your sendgrid username>
SENDGRID_PASSWORD=<your sendgrid password>
```

(Or set up equivalent environment properties.)

Then run `npm start`.

That's all it takes to get started! However, while you can use this script as-is, it's intended to be a starting point 
to do your own thing with your verizon points. (Bid on an auction, enter a different sweepstakes, or just rack up points 
without spending them.)

Heroku Usage
------------

This script can be run on a free [Heroku](http://www.heroku.com/) server with a little bit of setup. 
Complete instructions for how to use heroku is beyond the scope of this document, but they have 
[very good documentation](https://devcenter.heroku.com/). 

The following instructions require the [Heroku Toolbelt](https://toolbelt.heroku.com/).

First create an app:

    heroku apps:create [optional-app-name]
    
Add the cronjob addon:

    heroku addons:create scheduler
  
Open the cronjob config page:

    heroku addons:open scheduler
  
Set the cronjob to run the command `npm start` once per day. (Or perhaps more often if you're doing auction stuff.)

Note: travis has a bug where they assume a web server even though we didn't declare 
    
If it doesn't seem to be working, run `heroku run bash` to open a shell on a new server instance. Then you can try running different commands and see what's going on.

Optionally email yourself results:

    heroku addons:create sendgrid
    heroku config:set EMAIL=<your email>
    heroku config:set EMAIL_ON_SUCCESS=true

Finally, push your code and then disable the default web worker that heroku creates:

    git push heroku
    heroku ps:scale web=0


MIT License
------------

Copyright (c) 2014 Nathan Friedly - http://nfriedly.com/

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
