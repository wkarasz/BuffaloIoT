# Challenge Project

Imagine you're a bar owner, and you're looking to provide a better experience to your patrons.  Ideally, you'd like to be able to anticipate and predict when a patron is in need of a refill.  For the challenge, we're giving you "coasters" to embed the SensorTag.

Apply what you've learned in this build-a-thon and come up with a working solution that will notify your TIBCO sponsor when your glass is empty or is about to become empty.  Extra bonus points if you're able to infer whether or not it's a light or dark beverage.

There is no one way to go about this, so be creative and use what you know.

Some additional ways to approach the problem:

- The SensorTag has a built-in 3-axis accelerometer.  If the "coaster" is flipped over, the SensorTag values for orientation will flip.  Determine the 'up' orientation values and create an event when the values reverse.
- If the light value is near constant for a set number of counts, the patron is either done drinking or is a slow drinker.  Think about what light conditions might exist when a transparent glass is empty.
