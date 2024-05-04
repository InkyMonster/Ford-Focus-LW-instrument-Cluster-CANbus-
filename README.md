

#
# MS Speed can bus messages for Ford Focus LW clusters 
I wanted to use the cluster from the focus to link up to race smims. Seeing as no one (form what I have seen) has published what CAN bus messages interact with the cluster I ended up doing it myself. So hopefuly someone out there finds this useful! :) 

Just a heads up as stated my main goal was just to get the cluster working outside the car so there are a few messages in this list I don't 100% know what they do or are for but are needed to make it "work" that being said I have tried to break them down as much as possible.

As a side note I had not looked into any of the I-CAN messages at this point in time just the MS bus messages. 

## Getting Started:
There firstly the most obvious thing you will need is a board to send the CAN messages there are a few boards you can use like on of the more popular options the [SeedStudio Arduino CANbus Shield](https://wiki.seeedstudio.com/CAN-BUS_Shield_V2.0/) or somehting like I had used [CANable dongle](https://canable.io/) (I had flashed mine with the knock off PCAN firmware). But that being said as long as your board can suport 125KBPS messaging your good to go!


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
The meesages I have taken a look that are either fully or partialy decoded are:

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
    <td class="tg-c3ow" colspan="2">Airbag state and odomiter</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x1B0</td>
    <td class="tg-c3ow" colspan="2">Hill start assist system state (Manual and Auto?)</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x098</td>
    <td class="tg-c3ow" colspan="2">ABS, Stability and traction control, backlight brightness</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x042</td>
    <td class="tg-c3ow" colspan="2">Immobilizer status</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x060</td>
    <td class="tg-c3ow" colspan="2">Seat belt light</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x110</td>
    <td class="tg-c3ow" colspan="2">RPM and Speed</td>
  </tr>
  <tr>
    <td class="tg-c3ow">0x290</td>
    <td class="tg-c3ow" colspan="2">Break fluid status</td>
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
    <td class="tg-c3ow" colspan="2">Engine light</td>
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
    <tr>
    <td class="tg-c3ow">0x250</td>
    <td class="tg-c3ow" colspan="2">Oil light</td>
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

For many of the instruments to work along with a number of other functions you will need to place the cluster in the "running state". This message will need to be sent repeatably to keep the cluster awake. In the car this message was sent every 60ms (about 16-17hz) but that being said I have sent the message at 180ms intervals without issue.


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
    <td colspan="1">NUL</td>.
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
    <td class="tg-c3ow">Off</td>
    <td class="tg-c3ow">0x00</td>
  </tr>
</tbody>

Note: If only one "on" signal is sent the light will stay on for about 2 secnds so you will need to send the mesage repetedely to keep it lit. (This mesage is sent every 50ms / 20hz in the car)
