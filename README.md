

#
# MS CAN bus messages for Ford Focus LW clusters 
I wanted to use the cluster from the focus to link up to race smims. Seeing as no one (form what I have seen) has published what CAN bus messages interact with the cluster I ended up doing it myself. So hopeful someone out there finds this useful! :) 

Just a heads up as stated my main goal was just to get the cluster working outside the car so there are a few messages in this list I don't 100% know what they do or are for but are needed to make it "work" that being said I have tried to break them down as much as possible.

As a side note I had not looked into any of the I-CAN messages at this point in time just the MS bus messages. 

This is very much a work in progress I still need to look at fuel and headlights among other things. I will try to have them added when im not swamped with my studies.

## Getting Started:
Firstly the most obvious thing you will need is a board to send the CAN messages there are a few boards you can use like on of the more popular options the [SeedStudio Arduino CANbus Shield](https://wiki.seeedstudio.com/CAN-BUS_Shield_V2.0/) or the [CANable dongle](https://canable.io/) (I had used this one and flashed mine with the knock off PCAN firmware). But that being said as long as your board can support 125KBPS messaging your good to go!


## Hooking things up (2012 LW):

![Cluster connector](InstrementClusterFocusPinout.jpg) 


<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Pin</th>
    <th class="tg-c3ow">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">1</td>
    <td class="tg-c3ow" colspan="2">MS-CAN - </td>
  </tr>
  <tr>
    <td class="tg-c3ow">2</td>
    <td class="tg-c3ow" colspan="2">MS-CAN + </td>
  </tr>
  <tr>
    <td class="tg-c3ow">3</td>
    <td class="tg-c3ow" colspan="2">VBAT (12V)</td>
  </tr>
  <tr>
    <td class="tg-c3ow">4</td>
    <td class="tg-c3ow" colspan="2">I-CAN -</td>
  </tr>
  <tr>
    <td class="tg-c3ow">5</td>
    <td class="tg-c3ow" colspan="2">I-CAN +</td>
  </tr>
   <tr>
    <td class="tg-c3ow">6</td>
    <td class="tg-c3ow" colspan="2">NA</td>
  </tr>
  <tr>
    <td class="tg-c3ow">7</td>
    <td class="tg-c3ow" colspan="2">NA</td>
  </tr>
  <tr>
    <td class="tg-c3ow">8</td>
    <td class="tg-c3ow" colspan="2">NA</td>
  </tr>
    <tr>
    <td class="tg-c3ow">9</td>
    <td class="tg-c3ow" colspan="2">Park detect swithc</td>
  </tr>
     <tr>
    <td class="tg-c3ow">10</td>
    <td class="tg-c3ow" colspan="2">GND</td>
  </tr>
  <tr>
    <td class="tg-c3ow">11</td>
    <td class="tg-c3ow" colspan="2">NA</td>
  </tr>
    <tr>
    <td class="tg-c3ow">12</td>
    <td class="tg-c3ow" colspan="2">NA</td>
  </tr>
</tbody>
</table>



## MS Bus Meesage overview
The messages I have taken a look at that are either fully or partially decoded are:

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">ID</th>
    <th class="tg-c3ow">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">0x03A</td>
    <td class="tg-c3ow" colspan="2">Indicators, Washer Fluid level and steering assist </td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x080</td>
    <td class="tg-c3ow" colspan="2">The cluster "State/Wake" signal</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x040</td>
    <td class="tg-c3ow" colspan="2">Airbag state and odometer</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x1B0</td>
    <td class="tg-c3ow" colspan="2">Hill start assist system state (Manual and Auto?)</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x070</td>
    <td class="tg-c3ow" colspan="2">ABS, Stability and traction control, backlight brightness</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x1E0</td>
    <td class="tg-c3ow" colspan="2">Immobilizer status</td>
  </tr>
  <tr>
  </tr>
  <tr>
    <td class="tg-c3ow">0x110</td>
    <td class="tg-c3ow" colspan="2">RPM and Speed</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x290</td>
    <td class="tg-c3ow" colspan="2">Break fluid, Washer fluid and backlight (see note)</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x2A0</td>
    <td class="tg-c3ow" colspan="2">Without this the "Engine malfunction" alert is triggered</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x240</td>
    <td class="tg-c3ow" colspan="2">Park break (See message for more detail)</td>
  </tr>
    <tr>
    <td class="tg-c3ow">0x250</td>
    <td class="tg-c3ow" colspan="2">Engine light and Oil light</td>
  </tr>
    <tr>
    <td class="tg-c3ow">0x320</td>
    <td class="tg-c3ow" colspan="2">Fuel</td>
  </tr>
     <tr>
    <td class="tg-c3ow">0x300</td>
    <td class="tg-c3ow" colspan="2">Alternator light</td>
  </tr>     
     <tr>
    <td class="tg-c3ow">0x1B4</td>
    <td class="tg-c3ow" colspan="2">Headlight and Lamps</td>
  </tr>     
    <tr>
    <td class="tg-c3ow">0x1A4</td>
    <td class="tg-c3ow" colspan="2">Trip computer: Outside temperature</td>
  </tr>     
    <tr>
    <td class="tg-c3ow">0x1A8</td>
    <td class="tg-c3ow" colspan="2">Trip computer: Range remaining</td>
  </tr>     
  </tr>     

</tbody>
</table>



## Message Breakdown:

### 0x110 - RPM and Speed

<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>0x110</td>
    <td colspan="1">Unknown</td>
    <td colspan="1">Unknown</td>
    <td colspan="1">Unknown (Stat)</td>
    <td colspan="1">(Unknown (Stat)</td>
    <td colspan="2"> RPM </td>
    <td colspan="2">Speed</td>
  </tr>
    <tr>
    <td></td>
    <td colspan="1">0xC0</td>
    <td colspan="1">0x03</td>
    <td colspan="1">0x0A</td>
    <td colspan="1">0x00</td>
    <td colspan="2"> RPM </td>
    <td colspan="2">Speed</td>
  </tr>
</tbody>
</table>

Speed can be calculated as shown below:
```
Speed in KM/H = Speed x 96
```
Example to display 170Km/h
```
170 x 96 = 0x3FC0

B6 = 0x3F
B7 = 0xC0
```


RPM can be calculated as shown below:
```
RPM = RPM / 2
```

Example to display 2,500 RPM
```
2500 / 2 = 0x04E2
High byte = 0x04 | 0xC0
Low byte = 0xE2

B4 = 0xC4
B5 = 0xE2
```

### 0x080 - Cluster wake signal

<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>0x080</td>
    <td colspan="1">Unknown (Stat)</td>
    <td colspan="1">Unknown</td>
    <td colspan="1">Unknown </td>
    <td colspan="1">Unknown</td>
     <td colspan="1">Unknown</td>
      <td colspan="1">Unknown</td>
    <td colspan="1"> Unknown (Stat)</td>
    <td colspan="1">Unknown (Stat)</td>
  </tr>
    <tr>
    <td>Door Open</td>
    <td colspan="1">0x77</td>
    <td colspan="1">0x03</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x3D</td>
    <td colspan="1">0xC9</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x03</td>
    <td colspan="1">0x81</td>    
  </tr>
    <tr>
    <td>Ignition on</td>
    <td colspan="1">0x77</td>
    <td colspan="1">0x83</td>
    <td colspan="1">0x06</td>
    <td colspan="1">0x3F</td>
    <td colspan="1">0xD9</td>
    <td colspan="1">0x06</td>
    <td colspan="1">0x03 </td>
    <td colspan="1">0x81</td>
  </tr>
    <td>Running</td>
    <td colspan="1">0x77</td>
    <td colspan="1">0x03</td>
    <td colspan="1">0x07</td>
    <td colspan="1">0x3F</td>
    <td colspan="1">0xD9</td>
    <td colspan="1">0x07</td>
    <td colspan="1">0x03 </td>
    <td colspan="1">0x81</td>
  </tr>
</tbody>
</table>

For many of the instruments to work along with a number of other functions you will need to place the cluster in the "running" state. This message will need to be sent repeatably to keep the cluster awake. In the car this message was sent every 60ms (about 16-17hz) but that being said I have sent the message at 180ms intervals without issue.


### 0x03A - Indicators

<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>0x03A</td>
    <td colspan="1">Static</td>
    <td colspan="1">Indicator</td>
    <td colspan="1">Static</td>
    <td colspan="1">NUL</td>
    <td colspan="1">NUL </td>
    <td colspan="1">NUL</td>
    <td colspan="1">NUL</td>
    <td colspan="1">NUL</td>
  </tr>
    <tr>
    <td></td>
    <td colspan="1">0x80</td>
    <td colspan="1">Indicator</td>
    <td colspan="1">0x01</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00 </td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
  </tr>
</tbody>
</table>


The indercator state can be set as per the table below:


<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Indicator state</th>
    <th class="tg-c3ow">B1 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">Left Only</td>
    <td class="tg-c3ow">0x04</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Right Only</td>
    <td class="tg-c3ow">0x08</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Both</td>
    <td class="tg-c3ow">0x0C</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
</tbody>
</table>

Note: If only one "on" signal is sent the light will stay on for about 2 secnds so you will need to send the mesage repetedely to keep it lit. (This mesage is sent every 50ms / 20hz in the car)



### 0x040 - Airbag Light and Odometer

<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>0x040</td>
    <td colspan="1">Static</td>
    <td colspan="1">Odometer</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Airbag Light </td>
    <td colspan="1">Static</td>
  </tr>
    <tr>
    <td></td>
    <td colspan="1">0x66</td>
    <td colspan="1">Odometer</td>
    <td colspan="1">0x80</td>
    <td colspan="1">0xFF</td>
    <td colspan="1">0xBE </td>
    <td colspan="1">0x00</td>
    <td colspan="1">Airbag Light</td>
    <td colspan="1">0x00</td>
  </tr>
</tbody>
</table>


**Odometer:** This one is a strage one, the odometer readout disapears if this is not set.

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Odometer state</th>
    <th class="tg-c3ow">B1 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">Shown</td>
    <td class="tg-c3ow">0x02</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Hidden (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>

</tbody>
</table>

**Airbag light:** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Odometer state</th>
    <th class="tg-c3ow">B6 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Hidden</td>
    <td class="tg-c3ow">0x80</td>
  </tr>

</tbody>
</table>

Note: you will need to send the mesage repetedely to keep the desired state. This mesage is sent every 50ms / 20hz in the car.

### 0x300 - Alternator light

<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>0x300</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Alternator</td>
    <td colspan="1">Alarm?</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
  </tr>
    <tr>
    <td></td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">Alternator </td>
    <td colspan="1">Alarm</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
  </tr>
</tbody>
</table>


**Alternator:** This one is a strage one, the odometer readout disapears if this is not set.

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Alternator state</th>
    <th class="tg-c3ow">B4 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On(Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x80</td>
  </tr>

</tbody>
</table>

**Alarm:** The cluster emits a very loud alarm sound I have no idea what this is for and never have I heard the car make this noise. (I only found it buy tinkering with the messages)

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Alarm state</th>
    <th class="tg-c3ow">B5 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">Off (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">On</td>
    <td class="tg-c3ow">0x80</td>
  </tr>

</tbody>
</table>

Note: you will need to send the mesage repetedely to maintain the confgitured state the mesage is sent every 400ms / 2.5hz in the car.


### 0x070 - ABS, ESC and backlight brightness

<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>0x070</td>
    <td colspan="1">Static</td>
    <td colspan="1">Uknown</td>
    <td colspan="1">ABS & ESC Setting</td>
    <td colspan="1">Static</td>
    <td colspan="1">ESC Status</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
  </tr>
    <tr>
    <td></td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x98</td>
    <td colspan="1">ABS Track CTL setting</td>
    <td colspan="1">0x80</td>
    <td colspan="1">ESC Status</td>
    <td colspan="1">0xF4</td>
    <td colspan="1">0xE8</td>
    <td colspan="1">0x10</td>
  </tr>
</tbody>
</table>


**ABS Light:** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Light State</th>
    <th class="tg-c3ow">B2 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x04</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Slow Flash</td>
    <td class="tg-c3ow">0x06</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Fast Flash</td>
    <td class="tg-c3ow">0x07</td>
  </tr>
</tbody>
</table>


**ESC Setting** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Light State</th>
    <th class="tg-c3ow">B2 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x80</td>
  </tr>
</tbody>
</table>

**ESC Status** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Light State</th>
    <th class="tg-c3ow">B2 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x10</td>
  </tr>
    <tr>
    <td class="tg-c3ow">Slow Flash</td>
    <td class="tg-c3ow">0x40</td>
  </tr>
    <tr>
    <td class="tg-c3ow">Fast Flash</td>
    <td class="tg-c3ow">0x60</td>
  </tr>
</tbody>
</table>

Note: you will need to send the mesage repetedely to maintain the confgitured state the mesage is sent every 60ms / 16-17hz in the car.



### 0x240 - Handbreak Light
<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
 </tr>
</thead>
<tbody>
  <tr>
    <td>0x240</td>
    <td colspan="1">Unknown</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Handbreak</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
  </tr>
  <tr>
    <td></td>
    <td colspan="1">0xB0</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">Handbreak</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
  </tr>
</tbody>
</table>



**Handbreak:** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Light State</th>
    <th class="tg-c3ow">B3 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On (Default)</td>
    <td class="tg-c3ow">0xC0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x40</td>
  </tr>

</tbody>
</table>

Note: In conjunction with this message neededing the wake signal you will also need to send the 0x070 message in order for this to function correctly. The 0x240 message needs to be repeatably sent to maintain the set state it is sent every 120ms / 8hz in the car.


### 0x250 - Engine and Oil light
<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
 </tr>
</thead>
<tbody>
  <tr>
    <td>0x250</td>
    <td colspan="1">Engine Light</td>
    <td colspan="1">Oil Light</td>
    <td colspan="1">Static</td>
    <td colspan="1">Handbreak</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
  </tr>
  <tr>
    <td></td>
    <td colspan="1">Engine Light</td>
    <td colspan="1">Oil Light</td>
    <td colspan="1">0x00</td>
    <td colspan="1">Handbreak</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
  </tr>
</tbody>
</table>



**Engine Light:** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Light State</th>
    <th class="tg-c3ow">B0 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x20</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Flash</td>
    <td class="tg-c3ow">0x30</td>
  </tr>
</tbody>
</table>

**Oil Light:** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Light State</th>
    <th class="tg-c3ow">B1 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">On (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x20</td>
  </tr>
</tbody>
</table>

Note: In conjunction with this message neededing the wake signal you will also need to send the 0x070 message in order for this to function correctly. The 0x240 message needs to be repeatably sent to maintain the set state it is sent every 120ms / 8hz in the car.


### 0x1B0 - Hill start assist system state
<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
 </tr>
</thead>
<tbody>
  <tr>
    <td>0x1B0</td>
    <td colspan="1">0x01</td>
    <td colspan="1">0x50</td>
    <td colspan="1">0x27</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x80</td>
    <td colspan="1">0x00</td>
  </tr>
</tbody>
</table>

Sending this message will provent the dash throwing the "Hill start assist not avalible" alert this message is repeated every 100ms / 10hz in the car.

### 0x1E0 - Immobilizer system state
<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
 </tr>
</thead>
<tbody>
  <tr>
    <td>0x1E0</td>
    <td colspan="1">0x42</td>
    <td colspan="1">0x80</td>
    <td colspan="1">0x38</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x80</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x80</td>
    <td colspan="1">0x00</td>
  </tr>
</tbody>
</table>

Sending this message will provent the dash throwing the "Immobiliser malfunction service required" alert this message is repeated every 100ms / 10hz in the car.


### 0x2A0 - Engine Status message
<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
 </tr>
</thead>
<tbody>
  <tr>
    <td>0x2A0</td>
    <td colspan="1">0x06</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x3E</td>
    <td colspan="1">0x4F</td>
    <td colspan="1">0x80</td>
    <td colspan="1">0xE5</td>
  </tr>
</tbody>
</table>

No too sure what content of this message is however without it the cluster throwing a "Engine malfunction service now" alert. This CAN message is repeated every 300ms / 3.3hz in the car.

### 0x290 - Break fluid, Washer fluid and backlight (see note)
<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
 </tr>
</thead>
<tbody>
  <tr>
    <td>0x2A0</td>
    <td colspan="1">0x98</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x01</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x04</td>
    <td colspan="1">0x03</td>
    <td colspan="1">0x92</td>
    <td colspan="1">0x37</td>
  </tr>
</tbody>
</table>

Send this message to provent the cluster from displaying  "Break fluid level low service now" and "Washer fluid level low" alert. This message also has an effect on the displays brightness regardless of the message contence I havent quite figered it out yet. This CAN message is repeated every 300ms / 3.3hz in the car.




### 0x1A4 - Trip Computer: Outside air temp
<table>
<thead>
  <tr>
    <th>ID</th>
    <th>0</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
    <th>7</th>
 </tr>
</thead>
<tbody>
  <tr>
    <td>0x1A4</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
    <td colspan="2">Tempriture</td>
    <td colspan="1">Temp enable</td>
    <td colspan="1">Static</td>
    <td colspan="1">Static</td>
  </tr>
  <tr>
    <td></td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x00</td>
    <td colspan="2">Tempriture</td>
    <td colspan="1">Temp enable</td>
    <td colspan="1">0x00</td>
    <td colspan="1">0x01</td>

  </tr>
</tbody>
</table>


Tempriture is calculated as shown below
```
Tempriture in C = 512 + (temp in C x 4)
```
Example to display -4C
```
512 + (-4 * 4) = 496 or 0x1F0 in hex

B3 = 0x01
B4 = 0xF0
```

**Tempritutre display enable:** 

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow">Tempritutre State</th>
    <th class="tg-c3ow">B5 Byte</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">Off (Default)</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
  <tr>
    <td class="tg-c3ow">On</td>
    <td class="tg-c3ow">0x80</td>
  </tr>
</tbody>
</table>

Note this message is sent every 50ms / 20hz in the car.


------

