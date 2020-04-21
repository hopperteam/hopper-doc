# 1 UC: Subscribe to app

## 1.1 Brief Description
When a user has a notification including actions, he can click on the actions to execute them

# 2 Flow of Events
## 2.1 Basic Flow
- User clicks on a action on a notification
- Action will be exectued
- Optional: Notification will be executed

### 2.1.1 Activity Diagram
![Activity Diagram](./img/uc-start-action.svg)

### 2.1.2 Mock-up
![Mockup](./mockups/hopper_main.png)
In this mockup, the notification from telegram contains actions that can be clicked.

## 2.2 Alternative Flows
(n/a)

# 3 Special Requirements
(n/a)

# 4 Preconditions
## 4.1 Logged in
The user has to be logged in to the system.
## 4.2 User has at least one notification containing at least one action
The user has to have at least one notification with at least one action in order to be able to start this action

# 5 Postconditions
## 5.1 Action executed
The action was send to the app. The exact handling depends on the app
 
# 6 Extension Points
(n/a)
