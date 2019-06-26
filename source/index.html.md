---
title: API Reference

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to WTG documentation on the API system, allowing testbench simulation.

# Authentication connect

> To authorize connect to WTG api URL: "..."

```javascript
const WTG URL = ("...");

```
> Make sure to replace `... with correct URL` for authentication.

This API is open atm but masked by URL only, future impliments will have logon.

`Authorization: URL "..."`

<aside class="notice">
You must replace <code>...</code> with WTG API URL.
</aside>

# POST requests
## POST /sim_launch/{id}
>  POST /sim_launch/{id}

```javascript
{
   "launch": "..."
}
```
> Example should return the below if sucessfull.

```json
 {"launch": "npm start"}
```
This will launches the simulation through basic command in terminal.
### Discription
Id is needed if there is more than one simulation to launch another instance of simulation "001"

### Dependencies
Parameter | Description
--------- | -----------
Launch | Command that lauches the simulation
ID | Id is assigned to each simulation for reference

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


## POST /sim_step
>  POST /sim_step

```javascript
{
 "frame": "..."
}
```
> Example should return the below if sucessfull.

```json
 {"frame": 20}
```
Incromental value that will count and log the time period of the simulation from the start, each is specific to the individual simulation.
### Discription
Step can be used to measue the reaction time or a error time scale, when it took place and why. With the step system implimented a defined tiem perioud can be added for logic control and debugging.

### Dependencies
Parameter | Description
--------- | -----------
Step Incroment | The incromenting value that will log the frame and time the simulation is live

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


## POST /sim_stop/{id}
>  POST /sim_stop/{id}

```javascript
{
   "shut_down": "..."
}
```
> Example should return the below if sucessfull.

```json
 {"shut_down": "^c"}
```
This will stop the given simulation.
### Discription
This will allow us to close a specific resources if the test has crashed failed or an update need to be made, closure of the simulation is needed.

### Dependencies
Parameter | Description
--------- | -----------
Stop | This will close the referenced simulation, through id
ID | Id is used to command a spacific simulation by reference

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


## POST /sim_reset/{id}
>  POST /sim_reset/{id}

```javascript
{
   "reset": "..."
}
```
> Example should return the below if sucessfull.

```json
{
  "Shutdownb": {
    "shut_down": "^c"
  },
  "reboot": {
    "launch": "npm start"
  }
}
```
Restarts the termanl containing and maintaining is current id to log on the same file.
### Discription
Id is required to restart a specific simulation, this can be due to it crashing error or updates that need to be implinmented.

### Dependencies
Parameter | Description
--------- | -----------
Reset | Stops and restarts the referenced simulation
ID | Id is used to command a spacific simulation by reference

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


## POST /building_array
>  POST /building_array

```javascript
{
  "co-ordinance": "..., ..."
  },
  "distance": "150m"
}
```
> Example should return the below if sucessfull.

```json
{
  "co-ordinance": "52.63537, 42.7382"
  },
  "distance": "150m"
}
```
Building information and postion will be stored in the array. 
### Discripton
Distanceand co-ordinance of each corner giving us size. Each piece of information will post the the simulation resource they are wrapped in named by id.

### Dependencies
Parameter | Description
--------- | -----------
Building | Stores the ID and reference to the building object
Distance | Distance from the POD is recorder due to sensor range and reaction time
Co-ordinace | Co-ordinace will be taken of courners of Obj to give us the size

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


## POST /dynamic_object
>  POST /dynamic_object

```javascript
{
  "distance": "...",
  "speed": "...",
  "heading_North": "..."	
}
```
> Example should return the below if sucessfull.

```json
{
  "distance": "150m",
  "obj-speed": {
    "speed": "10 KMPH"
  },
  "heading_North": "10 degrease"
}
```
Stores Dynamic moving object

### Distcription
For collison avoidence they will be fed into the ACS stack so that it can make dicision within a reaction period wheather to stop or avoide the object. Making a safe and effective way of testing the POD, in a controlled inviroment.

### Dependencies
Parameter | Description
--------- | -----------
Distance | Distance from the POD is recorder due to sensor range and reaction time
Speed | Defines the velocity that the dynamic object is moving at for reference for objects course

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


## POST /traffic_signals
>  POST /traffic_signals

```json
{
  "distance": "...",
  "sign_action": "..."	
}
```
> Example should return the below if sucessfull.

```json
{
  "distance": "150m",
  "sign_action": "stop"
}
```
Traffic signals will be read using and stored.
### Discription
Econ camera systems and openCV that will distinguish the signs signals to the vehicle. Whether to stop, turn or carry on forward.

###Dependecies
Parameter | Description
--------- | -----------
Building | Stores the ID and reference to the building object
Distance | Distance from the POD is recorder due to sensor range and reaction time
Co-ordinace | Co-ordinace will be taken of courners of Obj to give us the size

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


## POST /junction
>  POST /junction

```json
{
  "distance": "...",
  "junction_action": "..."
}
```
> Example should return the below if sucessfull.

```json
{
  "distance": "150m",
  "junction_action": "left"
}
```
The oncoming junction in the simulation will be notified to the POD within a distance tolerance.
###Description
The junction action is posted to the ACS static for the desicion and track the POD takes, it is not dependant on objects but can be affected by an object.

### Dependencies
Parameter | Description
--------- | -----------
Distance | Distance from the POD is recorder due to sensor range and reaction time
Action | The next jusnction need to be pre identified by the simulation to know what action to take next not depending on obsticles

###Returns
<aside class="success"> 201: "ok"</aside>
<aside class="warning"> 400: "bad input parameter"</aside>


# GET requests
## GET /position
> GET /position

```json
{
   "id": "..."
}
```
> Example should return the below if sucessfull.

```json
{
  "position": {
    "longitude": "52,637",
    "latitude": "65,136"
  },
  "gridsquare": 21
}
```
This will return the position of the POD.
### Discription
The postion of the POD is stored in co-ordinace when the get command is processed it will take the posted information and return it in the GET in format Json.

### GET returns
Parameter | Description
--------- | -----------
Co-ordinace | Distance from the POD is recorder due to sensor range and reaction time


### Returns
<aside class="success"> 201: longitude "52,637", latitude "65,136", gridsquare "21"</aside>
<aside class="warning"> 404: "not found"</aside>


## GET /speed
> GET /speed

```json
{
   "id": "..."
}
```
> Example should return the below if sucessfull.

```json
{
  "speed": "10 KMH"
}
```
This will return the speed of the POD.
### Discription
The speed of the POD is stored in KMH when the get command is processed it will take the current speed and return it in the GET in format Json.

### GET Returns
Parameter | Description
--------- | -----------
Speed | Speed of POD in smulation passed to the ACS for control of teh ACS stack decision making

### Returns
<aside class="success"> 201: speed "10 KMH"</aside>
<aside class="warning"> 404: "not found"</aside>


## GET /steering
> GET /steering

```json
{
   "id": "..."
}
```
> Example should return the below if sucessfull.

```json
{
  "angle": "10 degrees"
}
```
This will return the steering angle on the POD.
### Discription
The steering angle of the POD is stored in the simulation at every step marker when the get command is processed it will take the steering angle and return it in the GET in format Json.

### GET returns
Parameter | Description
--------- | -----------
Angle | Angular heading of the POD in the simulation sent to the ACS stack for corrispondance

###Returns
<aside class="success"> 201: angle "10 degrees"</aside>
<aside class="warning"> 404: "not found"</aside>


## GET /vector
> GET /vector

```javascript
{
   "id": "..."
}
```
> Example should return the below if sucessfull.

```json
{
  "vector": {
    "speed": "10 KMH"
  },
  "angle": {
    "angle": "10 degrees"
  }
}
```
This will return the vetor of the POD.
### Discription
Vector is achieved from the steering and speed of the POD which combined give us a vectror of heading of the pod from its previous point, vectors tell you the vehichle geading in a 2d or 3D from
 trajectory and velocity.

### Get returns
Parameter | Description
--------- | -----------
Speed | Speed of POD in smulation passed to the ACS for control of teh ACS stack decision making
Angle | Angular heading of the POD in the simulation sent to the ACS stack for corrispondance

###Returns
<aside class="success"> 201: speed "10 KMH", angle: "10 degrees"</aside>
<aside class="warning"> 404: "not found"</aside>




