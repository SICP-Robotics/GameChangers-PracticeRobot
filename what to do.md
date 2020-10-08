## Task 0. Setup

### Subtask 0. Viewing This Document
Open VSCode (our IDE) and then press `CTRL + Shift + V`, which will open up a fancy view of tihs document. Also, if you need any help, don't forget that you can ask another coder (like Sam)!

### Subtask 1. Cloning Code
First, let's set up your coding environment, where you'll be doing to bulk of your coding. First, we need to **clone** our code from our git code repository, which holds our code and tracks changes. Our git repository is located on a remote server hosted by **GitHub**, and when we **clone** code we're basically just copying it off of there.

1. Open up GitHub Desktop. The icon looks like a white cat on a purple background.
2. Go to `File > Clone repository...`.
3. Click on the `GitHub.com` tab if not already selected.
4. Search for `PracticeRobot` in the search bar and select it. The full repo name should be something like `@SICP-Robotics/GameChangers-PracticeRobot`.
5. Check the location that it's cloning to and remember that location.
6. Click `Clone`.

### Subtask 2. Open the Code
1. Using VSCode, which is probably what you're viewing this document on, go to `File > Open Folder` and find the location where you cloned `PracticeRobot` to.
2. If you now see the code, you're good to go.

### Subtask 3. Build the Code
Our robot is written in Java using libraries provided by FIRST. The main library used is called *WPILib*. Since it's written in Java, we need to turn it from our human-readable Java code to machine-readable bytecode. We do that through a process called **building**. We automate our **build process** through a tool called Gradle. For the most part, you won't have to mess with Gradle directly.

1. Open up a terminal. You can do this by going to `Terminal > New Terminal`.
2. Type `./gradlew build` and then press enter.
3. You should see the green letters `BUILD SUCCESSFUL` in ther terminal after some time. Not that the first build might be really slow compared to the others.

### Subtask 4. Shortcuts
What you've just done is run the Gradle task `build`. Instead of typing that every time we want to build, though, we have a shortcut -- go the W icon in the top-right corner, click it and find `Build Robot Code`. Click it and it will build the code for you.

### Subtask 5. Deploying the Code
To actually put our code on the robot, we will use a process called **deploying**. Deploying consists of first building our code and then uploading it onto the robot. Again, Gradle will be managing this process for us.

1. Turn on the robot. You do this by squeezing the on/off switch. You'll probably need someone to show you how to turn it on.
2. Take note of the year on the radio. This is the white thing with the blinky lights. Again, you might want someone to show this to you. The year will be something like `2018A`, depending on what year the radio is from.
3. Open up the WiFi menu on the laptop and connect to the WiFi. We will be deploying our code over WiFi.
4. Go to the W icon and select `Deploy Robot Code`. Gradle will then 