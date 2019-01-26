# GPS-SDR-SIM

GPS-SDR-SIM generates GPS baseband signal data streams, which can be converted 
to RF using software-defined radio (SDR) platforms. In our research, we have used HackRF.

### gps-sdr-sim

This file includes ephemeris files, C/A generated code and other related data.

### Enter the code folder
```
$ cd gps-sdr-sim
```

### Building with GCC

```
$ gcc gpssim.c -lm -O3 -o gps-sdr-sim
```

### Get latitude and longitude information of a place

Access [GPS latitude and longitude](http://www.gpsspg.com/maps.htm)

### generate pseudocode 

```
$ ./gps-sdr-sim -e brdc3540.14n –l 31.603202,120.466576,100  -b 8
```
Following the command option, a “gpssim.bin” file will be added into the file, namely simulation of the generated GPS data.

```
Usage: gps-sdr-sim [options]
Options:
  -e <gps_nav>     RINEX navigation file for GPS ephemerides (required)
  -u <user_motion> User motion file (dynamic mode)
  -g <nmea_gga>    NMEA GGA stream (dynamic mode)
  -l <location>    Lat,Lon,Hgt (static mode) e.g. 30.286502,120.032669,100
  -t <date,time>   Scenario start time YYYY/MM/DD,hh:mm:ss
  -T <date,time>   Overwrite TOC and TOE to scenario start time
  -d <duration>    Duration [sec] (dynamic mode max: 300 static mode max: 86400)
  -o <output>      I/Q sampling data file (default: gpssim.bin ; use - for stdout)
  -s <frequency>   Sampling frequency [Hz] (default: 2600000)
  -b <iq_bits>     I/Q data format [1/8/16] (default: 16)
  -i               Disable ionospheric delay for spacecraft scenario
  -v               Show details about simulated channels
```

### Send forged data using HackRF

The simulated GPS signal file, named "gpssim.bin", can be loaded
into the HackRF for playback as shown below:

```
$ hackrf_transfer -t gpssim.bin -f 1575420000 -s 2600000 -a 1 –x.
```
