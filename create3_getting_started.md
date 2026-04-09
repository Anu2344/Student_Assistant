**iRobot Create® 3**

Getting Started --- Lab Guide

*Robot Setup, Light Ring, Wi-Fi & Bluetooth Connection*

# Basic Safety Rules

The Create® 3 is a mobile ground robot. Unlike robotic arms, it does not pose significant crush hazards, but basic precautions still apply:

-   Keep the robot on a flat, unobstructed surface. The robot will autonomously drive and may fall off edges or tables.
-   The robot uses cliff sensors to detect drop-offs, but do not rely solely on them --- always supervise the robot near table edges.
-   Do not place fingers under the robot while it is moving. The drive wheels can pinch.
-   If the robot behaves unexpectedly, press the center power button once to stop it, or simply pick it up.
-   If you are in doubt about any procedure, ASK for help BEFORE doing it.

# The iRobot Create® 3 Robot

The iRobot Create® 3 is a mobile robotics platform built on the Roomba i3 chassis, designed for university-level robotics education. It runs ROS 2 internally and supports programming via Wi-Fi, Bluetooth Low Energy (BLE), or USB-C Ethernet.

## Key Hardware Features

-   Multizone front bumper with 7 pairs of infrared (IR) proximity sensors
-   Four cliff sensors (underside) to detect surface drop-offs
-   Optical odometry sensor and IMU for position tracking
-   Two drive wheels with encoders and current sensors
-   Integrated speaker for audio feedback (startup chime, error tones)
-   Ring of 6 RGB LEDs around the center power button --- shows robot state
-   Removable faceplate and cargo bay with mounting holes for payloads
-   USB-C port for wired connection to external computers
-   Adapter board (under faceplate) with Bluetooth / USB-C switch

## Buttons

The Create® 3 has three buttons on its top face:

| **Button** | **Label** | **Function** |
|---|---|---|
| Button 1 | Single dot (•) | Hold 10 seconds → Standby mode (charging stays active). Wake: hold center button 1 sec. Can be used as a programmable user button. |
| Button 2 | Double dot (••) | User-programmable button only. Press events are accessible in ROS 2 and Bluetooth modes. |
| Center Button | Power icon (⏻) | Powers robot on/off. Hold 7 sec → Storage mode (battery disconnected; only dock can wake it). Ring of 6 RGB LEDs shows robot state. |

# Light Ring --- Status Reference

The ring of 6 RGB LEDs around the center button communicates the robot's state at all times. Learning to read the light ring is essential for diagnosing what the robot is doing.

## While Charging / Idle

| **Color / Pattern** | **Status** | **Meaning** |
|---|---|---|
| ⬜ White --- Spinning | Booting up | Wait for the startup chime ("happy sound") before interacting with the robot. |
| ⬜ White --- Partial Spin | Charging | The arc length represents charge level (e.g., roughly half arc = ~50%). |
| ⬜ White --- Solid | Fully charged / Powered on | Robot is ready to use. |
| 🔴 Red --- Pulsing | Low battery (<10%) | Place the robot on the charging dock immediately. |
| 🔴 Red --- Solid | Error | Robot encountered an error. Try cycling power (press center button). |

## While Connecting to Wi-Fi Access Point

| **Color / Pattern** | **Status** | **Meaning** |
|---|---|---|
| 🔵 Cyan --- Spinning | AP mode active | Robot is broadcasting its own Wi-Fi hotspot. Connect your computer to it. |
| 🔵 Cyan --- Solid | Computer connected to robot AP | Your computer has joined the robot's Wi-Fi. Open 192.168.10.1 in browser. |
| 🟢 Green --- Quick flash | Wi-Fi success | Robot has connected to your campus/lab Wi-Fi network. |
| ⬜ White --- Solid | AP closed | Robot disconnected from its own hotspot; now using campus Wi-Fi. |

Wi-Fi error codes (shown after a solid cyan phase):

| **Color / Pattern** | **Status** | **Meaning** |
|---|---|---|
| 🟡 Yellow + 🔴 Red | Bad password | Re-enter the Wi-Fi password carefully. |
| 🟡 Yellow + 🟢 Green | Cannot reach access point | Check the network name (SSID). Robot may be out of range. |
| 🟡 Yellow + 🔵 Blue | DHCP timeout | Try again. Network may be slow to assign an IP address. |
| 🟡 Yellow + ⬜ White | Association failed | Try again. Possible interference or overloaded access point. |
| 🟡 Yellow --- Solid | Unknown Wi-Fi failure | Try the whole AP connection process again from the start. |

## While Updating Firmware

| **Color / Pattern** | **Status** | **Meaning** |
|---|---|---|
| 🔵 Cyan --- Solid | Ready to update | Computer is connected to robot AP; web interface is open. |
| 🔵 Blue --- Spinning | Downloading update | Do not remove from dock. |
| ⬜ White --- Spinning | Installing firmware | Do not power off or remove from dock. |
| ⬜ White --- Solid | Update complete | Robot plays happy sound. Safe to proceed. |

## While Operating

| **Color / Pattern** | **Status** | **Meaning** |
|---|---|---|
| ⬜ White --- Spinning | Booting up | Wait for happy sound. |
| ⬜ White --- Solid | Normal operation | Default light when running. |
| 🔴 Red --- Pulsing | Battery < 10% | Dock the robot to charge. |
| 🔴 Red --- Spinning | Battery critical (<3%) | Robot will shut down very soon. Dock immediately. |
| 🟠 Orange --- Rear half | Backup safety active | Robot detected it was going to drive into something while reversing. |
| 🟡 Yellow --- Rear half | Wheels disabled | Wheels have been software-disabled. Check your code or restart. |

# Powering On the Robot

Follow these steps each time you start a lab session:

1.  Place the Create® 3 on the charging dock with the charging contacts aligned. The robot should click into place.
2.  Plug the dock cable into a power outlet. The robot will power on automatically.
3.  Wait for the light ring to stop spinning white and hear the startup chime ("happy sound"). This takes approximately 1--2 minutes.
4.  Once the light ring glows solid white, the robot is ready.

> **⚠️ Important:** If the robot is in storage mode (battery disconnected), you must place it on the dock first --- it cannot be powered on by pressing the button.

## Low Power Mode

If the robot's light ring shows pulsing red, the battery is below 10%. The robot will still respond to Wi-Fi and Bluetooth in this state, but dock it as soon as possible.

To exit Low Power Mode manually: hold the center button for 1 second.

# Connecting to Wi-Fi

Connecting the Create® 3 to your lab's Wi-Fi network allows you to program it over ROS 2 and use the robot's web interface from any computer on the same network.

> **ℹ️ Note:** You only need to complete this setup once. The robot remembers the Wi-Fi network between sessions.

## Step 1 --- Activate the Robot's Hotspot (AP Mode)

With the robot powered on and showing a solid white light ring:

5.  Press and hold both Button 1 (•) and Button 2 (••) together for 3 seconds.
6.  The light ring will begin spinning blue and the robot will play a sound --- this confirms AP mode is active.

## Step 2 --- Connect Your Computer to the Robot's Hotspot

7.  Open your computer's Wi-Fi manager.
8.  Look for a network named Create-67D0 (where 67D0 is your robot's unique identifier, found on its label).
9.  Connect to this network. It may take up to 2 minutes to appear.
10. When connected, the robot's light ring will change from spinning blue to solid cyan.

> **⚠️ Important:** Your computer will lose internet access while connected to the robot's hotspot. This is normal --- the robot's web interface does not need internet.

## Step 3 --- Open the Robot's Web Interface

11. Open a web browser (Chrome is recommended).
12. Navigate to: 192.168.10.1
13. The robot's web interface will load. This page runs on the robot itself --- no internet is needed.

## Step 4 --- Enter Your Wi-Fi Credentials

14. In the web interface, click the Connect tab.
15. Select your lab or campus Wi-Fi network from the list and enter the password.
16. Click Save.
17. Watch the light ring: it will spin cyan (attempting connection), then flash green briefly (success), then return to solid white.
18. The robot will disconnect from its own hotspot automatically. Your computer will reconnect to its usual network.

> **⚠️ Important:** If the light ring shows a yellow + color error code, refer to the Wi-Fi error code table in the Light Ring section above.

## Step 5 --- Verify the Connection

To confirm the robot is on the network, activate AP mode again (hold Buttons 1 + 2), connect your computer to the robot's hotspot, open 192.168.10.1, and check the Home tab --- it should display the robot's IP address on your lab network.

# Connecting via Bluetooth (Python Web Playground)

Bluetooth Low Energy (BLE) allows you to connect directly to the robot from a computer without any network setup. This is the quickest way to run your first Python program on the robot.

> **ℹ️ Note:** Bluetooth mode uses the iRobot Education Python Web Playground at python.irobot.com --- no installation required.

## Requirements

-   A computer or laptop with Bluetooth Low Energy support
-   Google Chrome browser (Bluetooth Web API is required --- Firefox and Safari do not support it)
-   The robot must be in Bluetooth mode (blue LED visible through the faceplate)

## Step 1 --- Enable Bluetooth on Your Computer

Ensure Bluetooth is turned on in your system settings before proceeding.

On Windows: Settings → Bluetooth & devices → toggle Bluetooth on.

## Step 2 --- Power On the Robot

19. Place the Create® 3 on the charging dock.
20. Wait for the startup chime and solid white light ring before proceeding.

## Step 3 --- Confirm Bluetooth Mode is Active

Look through the faceplate on the back-right side of the robot. You should see a small blue LED glowing on the Adapter Board --- this confirms the robot is in Bluetooth mode.

## Step 4 --- Open the Python Web Playground

21. Open Google Chrome.
22. Go to: https://edu.root.samlabs.com/what-we-offer/irobot-python
23. Click the Connect button at the top of the page.

## Step 5 --- Pair with the Robot

24. Chrome will open a Bluetooth device chooser dialog.
25. Wait approximately 30 seconds for your robot to appear in the list. It may show its name (e.g., Create-67D0), iRobot or as "Unsupported Device".
26. Select the robot and click Pair.

> **⚠️ Important:** If multiple robots are present in the room, confirm you are pairing with the correct one by checking the robot label or briefly covering the others' Bluetooth LEDs.

## Step 6 --- Run Your First Program

The Python Web Playground loads with a default example program. Click the Play button to run it.

# Updating Firmware (If Required)

Your instructor will tell you if a firmware update is needed. If so, follow these steps after opening the robot's web interface (192.168.10.1):

27. Navigate to the Update tab in the web interface.
28. Download the firmware package from the iRobot releases page if you have not already.
29. Upload the firmware file using the interface on the Update tab.
30. Watch the light ring: spinning blue (downloading) → spinning white (installing) → solid white (done).
31. Do not power off the robot or remove it from the dock during the update.

> **⚠️ Important:** The light ring may briefly flash red during a firmware update. This is normal. Wait for the solid white light and happy chime before doing anything.

# Powering Down

At the end of each lab session:

32. Stop any running programs on your computer.
33. Place the robot back on the charging dock.
34. Confirm the light ring shows charging state (partial white spin).
35. You do not need to power off the robot --- it will charge for the next session.

# Quick Troubleshooting Reference

| **Problem** | **Solution** |
|---|---|
| Light ring not turning on | Check that the charging dock is plugged in and the contacts are aligned. Try placing on dock. |
| Light ring spins white forever | The robot is still booting. If this lasts more than 5 minutes, cycle power by removing from dock for 30 seconds. |
| Create-xxx hotspot not appearing | Wait 2 more minutes. If still missing, hold Buttons 1+2 again. Check robot label for the correct SSID. |
| Cannot open 192.168.10.1 | Confirm your computer is connected to Create-xxx, not your campus Wi-Fi. Disable VPN if active. |
| Wi-Fi shows yellow + red error | Wrong password. Re-enter the Wi-Fi credentials in the Connect tab. |
| Wi-Fi shows yellow + blue error | DHCP timeout. Try the connection again. Ask your instructor if the problem persists. |
| Robot not appearing in Bluetooth list | Ensure Chrome is being used. Check the Adapter Board switch is on the Bluetooth icon. Wait 30 seconds. |
| Robot appears as Unsupported Device | This is normal --- select it and pair anyway. |
| Robot drives off the table / cliff | The cliff sensors may be dirty. Wipe the underside sensors gently with a dry cloth. Always supervise. |
| Solid red light ring | Robot error. Cycle power: remove from dock, wait 10 seconds, place back on dock. |

# Useful Links & Resources

-   Official iRobot Create® 3 Documentation: https://iroboteducation.github.io/create3_docs/
-   Python Web Playground (Bluetooth programming): https://python.irobot.com/
-   Light Ring & Buttons Reference: https://iroboteducation.github.io/create3_docs/hw/face/
-   Wi-Fi Setup Guide: https://iroboteducation.github.io/create3_docs/setup/provision/
-   Multi-Robot Setup: https://iroboteducation.github.io/create3_docs/setup/multi-robot/
-   Firmware Releases: https://iroboteducation.github.io/create3_docs/releases/overview/

*Based on iRobot Create® 3 official documentation --- iroboteducation.github.io/create3_docs/*
