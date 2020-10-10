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
2. Type `./gradlew build` and then press enter. This will run the Gradle task `build`.
3. You should see the green letters `BUILD SUCCESSFUL` in ther terminal after some time. Not that the first build might be really slow compared to the others.

### Subtask 4. Shortcuts
What you've just done is run the Gradle task `build`. Instead of typing that every time we want to build, though, we have a shortcut -- go the W icon in the top-right corner, click it and find `Build Robot Code`. Click it and it will build the code for you.

### Subtask 5. Deploying the Code
To actually put our code on the robot, we will use a process called **deploying**. Deploying consists of first building our code and then uploading it onto the robot. Again, Gradle will be managing this process for us.

1. Turn on the robot. You do this by squeezing the on/off switch. You'll probably need someone to show you how to turn it on.
2. Take note of the year on the radio. This is the white thing with the blinky lights. Again, you might want someone to show this to you. The year will be something like `2018A`, depending on what year the radio is from.
3. Open up the WiFi menu on the laptop and connect to the WiFi. We will be deploying our code over WiFi.
4. Go to the W icon and select `Deploy Robot Code`. Gradle will then build the code for you and put it on the robot.

### Subtask 6. Run the Code on the Robot
Now that our code is on the robot, we probably want to run it and test it out. 

1. Open up a program called `FRC Driver Station`. This is the program that we'll be using to interface with the robot, and it's the same thing that we use during competitions.
2. Plug in a joystick to the computer.
3. On the driver station, enable the robot. This will allow it to move.
4. Put a *slight* input on the joystick to see if the robot moves. If it does, success!

## Task 1. Writing Some Code
If you've never written Java code before, don't worry. We're going to keep this simple so that you can follow along, and we'll basically be giving you code to copy in. As a general rule of thumb, it's always nice to retype code that you see instead of copy/pasting it so that you learn it, so try typing things out -- and if you want to try tinkering with something, go ahead!

### Subtask 1. `Hello, world!`
Notice that on the left, we have a file tree of everything in our folder. We'll be using this menu to manage the different files in our project.

1. Using the file tree on the left, go to `src/main/java/frc/robot/RobotContainer.java`. At the top of the file, you should see:
    ```java
    // This is the robot container file!
    ```
    If you see this, you're in the right place!
2. Go to the place where it says `public RobotContainer()`. This is at line `42` (you can see line numbers on the left).
3. You should see something like this:
    ```java
    /**
    * The container for the robot. Contains subsystems, OI devices, and commands.
    */
    public RobotContainer() {
        driveTrain = new DriveTrain();
        driveTrain.setDefaultCommand(new DriveWithJoystick(driveTrain, this::getJoystickY, this::getJoystickX, this::getJoystickAdjust));

        // Configure the button bindings
        configureButtonBindings();
    }
    ```
4. Let's break down what we're looking at. The `public RobotContainer() { ... }` indicates that we're defining a method. This is a special method (called a **constructor**) that runs when the `RobotContainer` is initialized. The robot will automatically run this when it is powered on. We should note that everything after a `//` on the same line will be ignored by the computer, and everything between `/* ... */` will also be ignored. These are called comments, and it'll make it easier for us to explain our code.
    * The code between the two curly braces is run when the method is run. We can break it down into two chunks right now:
        ```java
        // This initializes the DRIVETRAIN, or the thing that makes the robot move
        driveTrain = new DriveTrain();
        driveTrain.setDefaultCommand(new DriveWithJoystick(driveTrain, this::getJoystickY, this::getJoystickX, this::getJoystickAdjust));

        // This configures the button bindings
        configureButtonBindings();
        ```
        We're not going to worry about the specifics right now, and don't feel bad if you don't understand any of it -- that's ok.
5. Add this to the method before everything else:
    ```java
    System.out.println("Hello, world!");
    ```
    So you should get something like this:
    ```java
    /**
    * The container for the robot. Contains subsystems, OI devices, and commands.
    */
    public RobotContainer() {
        // THE CODE YOU ADD:
        System.out.println("Hello, world!");

        // Code you don't touch:
        driveTrain = new DriveTrain();
        driveTrain.setDefaultCommand(new DriveWithJoystick(driveTrain, this::getJoystickY, this::getJoystickX, this::getJoystickAdjust));

        // Configure the button bindings
        configureButtonBindings();
    }
    ```
6. Deploy the code onto the robot.
7. Open up the driver station. You should see a console on the right. Right click it and hit `View console log`. This is basically your robot's debug output.
8. You should see your message `Hello, world!` in green somewhere in the console. Congrats!
9. Try experimenting with this. How do you think that you could make it say something like "Hello, world! My name is *(your name)*"?

### Subtask 2. Writing a Command
This is where things get more complicated, so if you don't know Java I suggest that you give yourself a pat on the back for getting this far and maybe look up some tutorials on the internet. If you know Java or are brave, you may continue.

Our robot is controlled by `subsystems`, which in turn are controlled by `commands`, which are all set up in the `RobotContainer`. The subsystems directly manage the robot's hardware and are where the low-level code lies. The advantage of using a system like this is that there won't be conflicts between two different things trying to use the same physical robot parts at the same time -- imagine the following scenario:

The robot is programmed to drive forwards for 1 second on button X and backwards for 1 second when button Y is pressed.

Now let's imagine that the operator presses X, and then while X is still running, presses Y. Since both control the same motors (the DriveTrain), what should happen? We probably want the robot to forget about the X input and start doing the Y, since we pressed that second. We do this through commands.

Every command "requires" subsystem(s). When that command is running, those subsystems can't be used by any other command. 

Going back to our example code, you may have noticed that the `driveTrain` subsystem has been set up for you:
```java
driveTrain = new DriveTrain();
driveTrain.setDefaultCommand(new DriveWithJoystick(driveTrain, this::getJoystickY, this::getJoystickX, this::getJoystickAdjust));
```
The first line here sets the variable `driveTrain` to a new `DriveTrain` subsystem.

The second line is a bit more complicated, but the important takeaway is the `.setDefaultCommand(...)` method. This sets the **default command** of the subsystem, i.e. the command that runs when there isn't any other command running that requires the subsytem. In our case, we're setting the default command to a  `DriveWithJoystick` command. This makes sense from a logical standpoint too -- if nothing else is using the drive train for something, we probably want to have the robot be controlled by the joystick.

Now, here's our actual task that you'll be doing: you'll be making a command that drives forwards for 1 second. Let's get started:
1. Find the `configureButtonBindings()` method. It should look like this:
    ```java
    /**
     * Use this method to define your button->command mappings. Buttons can be
    * created by instantiating a {@link GenericHID} or one of its subclasses
    * ({@link edu.wpi.first.wpilibj.Joystick} or {@link XboxController}), and then
    * passing it to a {@link edu.wpi.first.wpilibj2.command.button.JoystickButton}.
    */
    private void configureButtonBindings() {
        // Here's a button you can use:
        Button buttonA = operatorController.buttons.A;
    }
    ```
2. Add the following line:
    ```java
    buttonA.whenPressed(new RunCommand(() -> driveTrain.cheesyDrive(0.3, 0, -1)).withTimeout(1), driveTrain);
    ```
    This binds a `RunCommand` to the buttonA that uses the `cheesyDrive` method on the `driveTrain` to drive the robot forwards. The parameters of `cheesyDrive` are:
    1. speed
    2. rotation
    3. `-1` (this value should always be -1)
3. Deploy.
4. Plug in the operator controller and press A to see if it works! Make sure to have your finger over the `Disable` button (or the enter key) in case something goes wrong.