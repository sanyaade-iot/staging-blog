---
layout: post

title: Spark.subscribe + hackster.io
cover_image: blog-cover.jpg

excerpt: "Core-to-Core pub-sub push messaging released in core-firmware v0.2.2. New Spark Projects site powered by hackster.io!"

author:
  name: Zachary Crockett
  twitter: towynlin
  bio: Founder, CTO
  image: zachary.jpg
---

## Spark.subscribe()

The Spark team is super proud to release in
[v0.2.2](https://github.com/spark/core-firmware/releases/tag/spark_5)
a much anticipated feature: `Spark.subscribe()`.
Now it's easier than ever to pass messages from one Core to another.

If you've worked with `Spark.function()`, this will look very familiar.
Just write your own event handling function, and register it in `setup()`.
Here's an example where the event handler is called `ledOn()`:

```
int onTime = -10000;

void ledOn(const char *event, const char *data) {
  onTime = millis();
}

void setup() {
  pinMode(D7, OUTPUT);
  Spark.subscribe("light-up", ledOn, MY_DEVICES);
}

void loop() {
  bool isOn = digitalRead(D7);
  if (millis() - onTime < 1000) {
    if (!isOn) {
      digitalWrite(D7, HIGH);
    }
  } else {
    if (isOn) {
      digitalWrite(D7, LOW);
    }
  }
}
```

In `setup()` I subscribe to the "light-up" event.
By adding `MY_DEVICES` to the subscription call,
I make sure other people's Cores can't turn on my LED.
Now whenever any of my Cores publishes "light-up",
the Cloud will send that event to my Core, which will call `ledOn()`

The `loop()` just checks whether we updated the variable `onTime` within the last second.
If so, and if the LED is off, we turn it on.
The else clause just turns the LED off one second later.

Now I install the following firmware on a different Core to publish the "light-up" event.

```
int last;

void setup() {
  pinMode(D7, OUTPUT);
  last = millis();
}

void loop() {
  if (millis() - last > 10000) {
    digitalWrite(D7, HIGH);
    delay(1000);
    digitalWrite(D7, LOW);
    Spark.publish("light-up");
    last = millis();
  }
}
```

Every ten seconds the LED turns on for one second.
The instant it turns off, the Core publishes a "light-up" event.
Here's a video of it working.
The Spark Core on the right publishes; the one on the left subscribes.

<iframe src="//player.vimeo.com/video/95062541" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen="allowfullscreen">&nbsp;</iframe>

Check out the [full `Spark.subscribe()` documentation](http://docs.spark.io/#/firmware/data-and-control-spark-subscribe).


## Spark Projects powered by hackster.io

We have partnered with the team over at hackster.io to create the official place to post your awesome Spark Core projects.
