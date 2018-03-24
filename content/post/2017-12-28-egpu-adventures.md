---
title: "macOS 10.13.2 EGPU Adventures"
date: 2017-12-28
draft: false
categories : [
    "Tinkerer",
]
tags: ["EGPU", ]
aliases:
  - "/2017-12-28-macos-egpu-adventures.html"
---

# 1) What is an EGPU & when did Apple start supporting them?

The acronym EGPU stands for external [GPU](https://en.wikipedia.org/wiki/Graphics_processing_unit). Until recently they were relatively niche however, with the release of thunderbolt3 they have begun to gain traction. At WWDC17 Apple announced that they would be fully supported in High Sierra sometime during the spring of 2018. This news was welcomed at [egpu.io](egpu.io) where a community of capable individuals have been trail blazing EGPUs on macOS [prior to 10.13](https://EGPU.io/setup-guide-external-graphics-card-mac/) & Windows. They quickly updated some of their [guides and recommendations](https://EGPU.io/macos-high-sierra-official-external-gpu/) to help beginners, such as myself, start their EGPU journey on High Sierra.

# 2) My setup

So after reading about the success and watching several youtube reviews I thought it was time to give this EGPU thing a go. For my enclosure I decided to go with the [Mantiz Venus](http://amzn.to/2CgKwQR) ($399). For my graphics card I decided to go with the [Vega64](http://amzn.to/2Ci1wpR). As a side note it looks like some users have had success with Nvidia cards on macOS after some elbow grease but AMD cards were reported to be plug and play; hence my decisions to go with AMD.

# 3) Initial experiences

After plugging it in and turning it on for the first time I was excited to see that everything was working out of the box.

![plug_n_play](/img/20171228_egpu_plug_n_play.png)

The only oddity that I noticed at first is that system information lists the Vega64 as "AMD RX xxx". However, his appears to only be a cosmetic issue so I ignore it.

![system_information](/img/20171228_system_information.png)

So after my initial excitement I tried playing a couple games with my new setup and quickly stumbled across something I should have uncovered sooner in my research. The Vega64 is quite power hungry and the enclosure I purchased [doesn't actually support it, it only supports Vega56](https://myMantiz.com/pages/faq).

For reference the problem that you'll encounter is that the entire enclosure will shut down which results in a soft or sometimes a hard system crash. So for those are thinking about purchasing the Mantiz & Vega make sure to go with the Vega56 rather than the Vega64. However, if you are like me and already have a Vega64 and/or you want to try an unsupported setup keep reading.

# 4) Resolving the power draw issue.

After some more research I found a new [power supply](https://www.newegg.com/Product/Product.aspx?Item=N82E16817273013) ($190) that would provide the needed power & had the same dimensions as the power supply that ships with the Mantiz. I'm happy to report that installing this part turned out to be essentially painless. The existing power supply comes out without much fuss and the new power supply fits perfectly in place of the old one. The only exception here is that the new power supply is a little longer than the existing one but there is ample room in the enclosure to accommodate this.

# 5) Subsequent experiences

After upgrading the power supply I've yet to experience another power related crash and have had a far more enjoyable experience.

The only remaining issue that I've had is a rare crash. Twice I've had macOS freeze for several seconds followed by a flash which results in all of my applications being closed (according to the dock, force-quite dialogs, & command-tab) but leaving the underlying processes untouched. This results in a bizarre situation where I can't view my application however, I can still hear the audio and see the process running in activity monitor. I expect/hope that this is one of those things that will be squashed once Apple rolls out official EGPU support in the spring with 10.13.x.

# 6) Benchmarks

What review of an EGPU setup would be complete without some benchmarks? Given the wide variety of applications & uses for an EGPU I decided to stay simple with some Geekbench benchmarks.

Using the AMD Pro 555 in my macbook-pro I received a score of [37,697](https://browser.geekbench.com/v4/compute/1670314)

![internal_score](/img/20171228_internal_score.png)

Using my EGPU setup I received a score of [175,303](https://browser.geekbench.com/v4/compute/1670320) a 4.65x improvement over the internal GPU offered by Apple. Quite the improvement!

![external_score](/img/20171228_external_score.png)

# 7) Final Thoughts

## Pros
* Performance
    * The Geekbench results show a 4.65x increase and my experiences with this increase have been tremendously positive
* Flexibility
    * If I need my laptop to be portable it is as simple as unplugging a cord
    * If I need my laptop to be ultra-fast it is as simple as plugging in a cord
* Upgradability
    * With this setup my Apple laptop now has an upgradable GPU which means I can keep my machine going for longer
* Ports
    * One of the nice things about the Mantiz enclosure is that it provides a lot of ports (5 USB & 1 gigabit ethernet port) and even includes a spot for a [2.5" SSD Drive](https://www.amazon.com/gp/search?ie=UTF8&tag=justnumbersan-20&linkCode=ur2&linkId=f73bf29f7e5ed526f77b4bfb06ae1826&camp=1789&creative=9325&index=electronics&keywords=SSD)
    * So rather than buying more dongles you can utilize the Mantiz as a hub as well

## Cons
* Weight
    * One thing that caught me off guard was just how heavy the enclosure & GPU were
    * It is far lighter than a desktop tower but still heavy enough to dissuade any thoughts of lugging it around
* Drivers
    * I thought that the Vega series would have first class support as an EGPU because of the Vega's inclusion in the iMac Pro however, since system information doesn't accurately identify the card it is clear that some support is still yet to come, likely in the spring
* Support
    * If you go with the Vega or really any other setup other than the [Apple EGPU kit](https://developer.apple.com/development-kit/external-graphics/) you are in an area that isn't officially supported
    * That being said you won't be alone or the first so don't let that hold you back too much

In summary I'd recommend an EGPU to anyone who is looking for a more robust GPU. The Pros are very compelling and the cons while worth considering don't represent a significant cost. The only other thing I'll call out is that I'd recommend the [Vega56](http://amzn.to/2C4u4Gw) + [Mantiz](http://amzn.to/2CgKwQR) rather than the [Vega64](http://amzn.to/2Ci1wpR) + Mantiz given the Vega64 requires an unsupported/warranty-breaking modification.
