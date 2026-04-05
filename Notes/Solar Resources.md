---
categories:
- '[[Personal]]'
tags:
- solar-system
---
- [Smart/Heavy Port Settings Issue ](https://www.youtube.com/watch?v=WsEsGSZIMq4)



- Allow grid charging will charge the battery until the **Battery Reserved percentage is attained**
- "On Grid Always On" and "Off grid always off" settings override the ON, OFF percentage settings in the Smart Port Settings
- **SoC** or **Overdischarge** is the percentage at which point, battery will not be discharged further to keep battery healthy. If its value is set to, let's say, 10% (90% DoD), then there's a risk of getting the battery completely discharged to 0, in case it doesn't receive any power for extended period. To prevent it, **force charge** setting allows to charge the battery to a health level to keep the battery from hitting the 0.
	- So let's say your battery SoC is set to 10%, but is at 5% charge.
	- If no power is received for long, the battery drops to 0, and is difficult to revive it.
	- Therefore, Force Charge, kicks in and uses whatever power mode available, without waiting for the Solar Power to be available to push it to a healthy state.