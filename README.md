# UE4 Hololens 2 Experiments
A set of reuseable Blueprint scripts and components to test Hololens capabilities in Unreal. 

Key features include "Grabbity", Half-Life:Alyx style grabbing mechanic, hand/joint drawing for debug, gesture tracker, fingertip+palm+wrist for physics interactions, etc

Here's a quick demo recorded directly from HoloLens 2:

[![Demo Video](https://img.youtube.com/vi/ifp68o6eSgM/0.jpg)](https://youtu.be/ifp68o6eSgM)

# Pre-requisites
- Unreal Engine 4.25
- Visual Studio 2017 with UWP C++ components installed
- Windows 10 SDK Version 10.0.18362.0

# Quick Start
1. In Project Settings > Platform > Hololens, in the "Packaging" section, ensure you have a signing certificate, if none, generate a new one here.
2. Package project in File > Package Project > Hololens
3. Use the WIndows Device Portal to install the generated appx bundle as described here: https://docs.microsoft.com/en-us/windows/mixed-reality/using-the-windows-device-portal

# What's included
**1. AR_Grab_Component:** Attach to motion controller to get grabbing functionality. Precision and Snap To Origin grabs currently supported.
 
To make an object grabbable by the component:
Pre-requisite: Your object must be a Bluperint Actor

> a. In Project Settings > Engine - Collision, create a new object channel called "Grabbable" with defautl response set to "Overlap"

> b. In the static mesh component (or other component with collision support) of the Actor you wish to make grabbable, set Collision Preset to "Custom", "Query Only" and Object Type to "Grabbable"

> c. In the main toolbar, "Class Settings"  of the Actor you wish to make grabbable, under "Interfaces", Add BPI_Grabbable

> d. Optional: Implement the functions of BPI_Grabbable to suit your needs (e.g. change material, add sound, etc in key events of the grab mechanic)

**2. BPI_Grabbable:** Add this to a Blueprint Actor as one of the requirements in making it respond to player grabs. You can implement Pre-Grab, Post-Grab, Pre-Release, Post-Release functions that will be triggered during these events. Useful for customizing behavior and/or add fx to the grab mechanic.

**3. BP_Grabbity:** Add this as a child actor under a Motion Controller Component to give your player Half-Life: Alyx style grabbing capabilities.

To make an object "grabbity-able":
Pre-requisite: Your object must be a Bluperint Actor
> a. Follow steps 1.a-d in the section for the grab component
> b. In the main toolbar, "Class Settings"  of the Actor you wish to make "grabbity-able", under "Interfaces", Add BPI_Grabbity
> c. Optional: Implement the functions of BPI_Grabbity to suit your needs (e.g. change material, add sound, etc in key events of the grab mechanic)

**4. BPI_Grabbity:** Add this to a Blueprint Actor as one of the requirements in making it respond to Half-Life:Alyx style player grabs. You can implement PreLockOn, PostLockOn, PreLockRelease, PostLockRelease and Reset functions that will be triggered during these events. Useful for customizing behavior and/or add fx to the grabbity mechanic.

**5. HL_FunctionLibrary:** Hololens function library you can use across your project. 

Available fucntions:
> a. Draw Debug Hand: Call this every tick on your pawn to draw a configurable hand rendering. This hand rendering is only available durign debug or development builds.

**6. FHandDebugOptions:** A custom struct that defines custom hand debug options (e.g. bone color, join color, joint shape segments, etc)

**7. BP_Gesture_Tracker:** Add this as a child actor under a Motion Controller Component so you can detect hand gestures that's not available via the SDK or not made available in BP (implemented smaple i nthis project is is Fist and finger point gesture)

**8. BP_Fingertips:** Add this as a child actor under a MOtion Controller Component to enable blocking collisions on key joints of a players hands, optionally the wrist and palm as well.

**9. HL_Pawn:** A demo HoloLens pawn that incorporates al lthe functions and scripts in this project

**10. AR_GameMode:** A demo GameMode that sets the default pawn to HL_Pawn and Starts an AR Session as well as enable Capture Gestures for Hololens 2 (See Event Graph)

**11. AR_SessionConfig:** A demo AR Session Config data asset with default values needed by the "Start AR Session" BP Node in AR_GameMode

**12. BP_GrabbableCube:** Sample Actor that's configured to be both Grabbable via the Half-Life:Alyx style Grab mechanic

**13: BP_WoodBlock:** Simple static mesh actor with blocking collisions enabled to test hand physics via BP_Fingertips

**14: TestMap_001:** Main test map to try out hand physics and Hal-Life:Alyx style grab mechanics.

**15: TestMap_Grabbity:** Test map to test HalfLife:Alyx style grab mechanics

# Credits/License
Entire project is under the MIT LICENSE

Copyright 2020 Beyond Reality Labs Pty Ltd (https://beyondreality.io)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---
Sample materials and meshes come from UE4 Starter Content, Editor Content, Engine Content and the Engine's VR Template - all under Epic Games License.
