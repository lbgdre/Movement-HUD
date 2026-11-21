# Installation

1. Extract the `cstrike` folder from the ZIP file to your game's root directory (normally: `\Half-Life\`)

2. Open the `plugins.ini` file (located in: `\cstrike\addons\amxmodx\configs\`)

3. Add the following 4 lines to the file:

- `mhud_menu.amxx`

- `mhud_speed.amxx`

- `input_overlay.amxx`

- `distance_prediction.amxx`
  
4. Save the file and restart your game

# Commands

## General

- `/mhud` - Open Plugin Settings Menu

## MHUD Speed

- `/mspeed` - Enable/Disable MHUD Speed

- `/mspeeds` - Open MHUD Speed Settings Menu

## Input Overlay

- `/mkey` - Enable/Disable Input Overlay

- `/mkeys` - Open Input Overlay Settings Menu

## Distance Prediction

- `/dp` `/distpred` - Enable/Disable Distance Prediction

- `/dps` - Open Distance Prediction Settings Menu

- `/sonar` - Enable/Disable Sonar

- `/rtpredhud` - Enable/Disable Real-Time Prediction HUD

- `/bestpredhud` - Enable/Disable Best Predicted Distance HUD

- `/landingpred` - Enable/Disable Landing Area Prediction

- `/ljpred` - Long Jump

- `/hjpred` - High Jump

- `/cjpred` - Count Jump

- `/scjpred` - Stand-Up Count Jump

- `/dcjpred` - Double Count Jump

- `/mcjpred` - Multi Count Jump

- `/wjpred` - Weird Jump

- `/sbjpred` - Stand-Up Bhop Jump

- `/bjpred` - Bhop Jump

- `/ldjpred` - Ladder Jump

- `/dpmethod` `/expected` - Switch the prediction method between Predicted and Expected (also item 8 in `/dps`)

# Expected distance (this fork)

The original prediction ("Predicted") assumes you stop strafing right now and fly straight on at your current velocity. This fork adds a second method, **Expected**, which assumes you keep strafing the way you have so far in this jump:

- **Gain rate** `c = (s² − s0²) / air time`, where `s0` is the takeoff speed and `s` the current horizontal speed.
- **Efficiency** `η = a / path`: the straight distance from takeoff divided by the path actually flown.
- Once two strafes are finished, both come from the last two finished strafes instead: `c` is their speed² gain rate (with the speed taken on that steady-gain line), and `η = (sin θL + sin θR) / (θL + θR)`, where `θL`, `θR` are the largest left and right angles between the velocity and the straight line through those two strafes.
- **Efficiency ramp**: the efficiency rises from `η` now to 1 at landing. From strafe 4 on it follows `(t/T)^2` instead of a straight line, because players keep turning hard until the last few strafes.

`Expected = a + (1 − loss) · L+ + 32`
