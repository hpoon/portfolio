---
layout: post
title: "Running League of Legends in PlayOnLinux (Ubuntu 14.04)"
categories:
  - Programming
  - Linux
  - Gaming
image: assets/images/playonlinux.png
description: "Complete guide to running League of Legends on Ubuntu 14.04 using PlayOnLinux and Wine"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2015/03/08/running-league-of-legends-in-playonlinux-ubuntu-14-04/](https://blog.henrypoon.com/blog/2015/03/08/running-league-of-legends-in-playonlinux-ubuntu-14-04/)

There are various guides floating around on the Internet for running League of Legends on Linux, and no single guide worked for me, but after piecing the information together from various places, I managed to get it to work on my system.

My computer specifications:

- Intel Core i5-4570
- 16 GB Memory
- Radeon HD 5770

I followed the instructions [here](http://askubuntu.com/questions/459888/shop-and-in-game-item-shop-not-working-in-league-of-legend-lol/461256#461256), with these changes:

- Using video driver "fglrx-updates" (the tutorial talks about NVIDIA cards)
- Did not install TuxLoL
- Did not do anything regarding the "Maestro error" since it only applies to Optimus Notebook users
- Did not follow step 6 because I did not run into the problem for big item icon text for the item shop
- **EDIT:** Thanks to Ingvar's comment, the installation progress for the game can be viewed like so: open terminal (Ctrl+Alt+T) and execute:

```bash
tail -f ~/.PlayOnLinux/wineprefix/LeagueOfLegends/drive_c/Riot\ Games/League\ of\ Legends/Logs/Patcher\ Logs/*.log
```

There are also other steps that I had to do, which I read from [here](https://www.playonlinux.com/en/app-1135-League_Of_Legends.html):

- Click configure for the "League of Legends" entry in "PlayOnLinux" and find the "Display" tab and then choose the following options:
  - Direct Draw Renderer - gdi
  - Video memory size - 4096 (or something else depending on graphics card)
  - Offscreen rendering mode - fbo\0
  - Everything else on default

- Create a file called `game.cfg` in the directory `/home/your-username-here/PlayOnLinux's virtual drives/LeagueOfLegends/drive_c/Riot Games/League of Legends/Config`. Below is what I have in my `game.cfg`:

```ini
[General]
EnableAudio=1
GameMouseSpeed=10
UserSetResolution=1
BindSysKeys=0
SnapCameraOnRespawn=0
OSXMouseAcceleration=1
AutoAcquireTarget=0
EnableLightFx=0
WindowMode=0
ShowTurretRangeIndicators=0
PredictMovement=0
WaitForVerticalSync=0
Colors=32
Height=1080
Width=1920
SystemMouseSpeed=0
CfgVersion=5.3.296
x3d_platform=1

[HUD]
CameraLockMode=0
MiddleClickDragScrollEnabled=0
KeyboardScrollSpeed=0.5000
ChatScale=50
ObjectTooltips=0
AutoDisplayTarget=0
ShowAllChannelChat=1
ShowTimestamps=1
ItemShopPrevY=39
ItemShopPrevX=106
NameTagDisplay=1
ShowChampionIndicator=0
ShowSummonerNames=1
ScrollSmoothingEnabled=0
MiddleMouseScrollSpeed=0.5000
MapScrollSpeed=0.5000
ShowAttackRadius=0
NumericCooldownFormat=1
SmartCastOnKeyRelease=0
EnableLineMissileVis=0
FlipMiniMap=1
ItemShopResizeHeight=0
ItemShopResizeWidth=164
ItemShopPrevResizeHeight=1080
ItemShopPrevResizeWidth=1920
ItemShopItemDisplayMode=1
ItemShopStartPane=1

[Performance]
CharacterInking=1
ShadowsEnabled=1
EnableHUDAnimations=0
PerPixelPointLighting=0
EnableParticleOptimizations=0
BudgetOverdrawAverage=0
BudgetSkinnedVertexCount=0
BudgetSkinnedDrawCallCount=0
BudgetTextureUsage=0
BudgetVertexCount=0
BudgetTriangleCount=0
BudgetDrawCallCount=0
EnableGrassSwaying=0
EnableFXAA=0
AdvancedShader=0
FrameCapType=6
GammaEnabled=0
Full3DModeEnabled=0
AutoPerformanceSettings=0
CharacterQuality=4
EffectsQuality=4
EnvironmentQuality=4
ShadowQuality=4
GraphicsSlider=6
paths=0

[FloatingText]
EnemyTrueDamageCritical_Enabled=1
EnemyMagicalDamageCritical_Enabled=1
EnemyPhysicalDamageCritical_Enabled=1
TrueDamageCritical_Enabled=1
MagicalDamageCritical_Enabled=1
PhysicalDamageCritical_Enabled=1
Countdown_Enabled=0
EnemyTrueDamage_Enabled=0
EnemyMagicalDamage_Enabled=0
EnemyPhysicalDamage_Enabled=0
TrueDamage_Enabled=0
MagicalDamage_Enabled=0
PhysicalDamage_Enabled=0
Score_Enabled=0
QuestComplete_Enabled=0
QuestReceived_Enabled=0
Disable_Enabled=0
Level_Enabled=0
Dodge_Enabled=0
Heal_Enabled=0
Special_Enabled=0
Invulnerable_Enabled=0
Debug_Enabled=0
Absorbed_Enabled=0
OMW_Enabled=0
EnemyCritical_Enabled=0
MagicCritical_Enabled=0
Critical_Enabled=0

[Volume]
SfxVolume=0.5
MasterVolume=0.5
```
