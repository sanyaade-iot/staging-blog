# Sprint 9

## CC3000 patch deployment planning

The cloud team went into the war room this sprint.
Texas Instruments is finishing the quality assurance testing on the CFOD patch,
and it should be released very soon.
We needed to figure out how to deploy it, safely and as seamlessly as possible,
to as many users as possible, including those who don't even know what CFOD is.

The whiteboard walls of our conference room were covered with some pretty crazy scribbles,
and the debate was intense.
The perfect balance was difficult to strike.
On one hand, we would love to upgrade every Core completely invisibly
since this update is so crucial.
On the other hand, that's both dangerous (potentially bricking the CC3000 unrecoverably)
and annoying for users who expect their firmware to be constantly running without interruption.
Once the whole technical situation had been laid out to everyone's satisfaction
we started making a list of things we agreed on.

* The update has to be opt-in, with users specifically clicking a button to see instructions and perform the patch.
* For Cores that currently perform OTA updates reliably, the patch should happen via a special button in the web IDE.
* There must also be a local USB patching option.


## Firmware version 0.2.1

* OTA reliability improvements
  ([core-firmware](https://github.com/spark/core-firmware/pull/155),
  [core-common-lib](https://github.com/spark/core-common-lib/pull/19),
  [core-communication-lib](https://github.com/spark/core-communication-lib/pull/8))
* Allow Spark.publish inside Spark.function
  ([core-communication-lib](https://github.com/spark/core-communication-lib/pull/13))
* Add Network.ping() ([core-firmware](https://github.com/spark/core-firmware/pull/156))
* Enable factory reset from firmware (only on new bootloader)
  ([core-common-lib](https://github.com/spark/core-common-lib/pull/21),
  [bootloader](https://github.com/spark/bootloader/pull/9))

## Heartbleed mitigation

We upgraded openssl to safe versions on all servers we control,
including specifically the web-facing ones like api.spark.io and community.spark.io on April ???.
We tried rotating the community certificate to one using an ECDSA key
for the extra-modern protection including mandatory forward secrecy,
but found many users' systems were incompatible.
All Spark TLS certificates were replaced today April 18.
