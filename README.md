# UAVSARhdr

UAVSARhdr is a simple python script to create a header file to accompany orthorectified UAVSAR binary images. A blog post describing its purpose and use was first written in 2014 and has ben updated where necessary and is provided below.

## Basic Usage

UAVSAR data is provided in grid (.grd) format without accompanying header file. To automatically generate one UAVSARhdr.py has been written. The Python script requires 3 command line option inputs:

**_-i_** – INPUT TXT FILE: The image parameters text file which is parsed by the script

**_-r_** – INPUT RADAR FILE: The input radar UAVSAR image in ‘.grd’ format. The image file is not opened or processed in any way but is used merely to create a header file with a name that matches the radar image

**_-p_** – IMAGE POLARIZATION: The polarization of the scene is required as cross-pol and co-pol imagery will have different data types. The co-pol imagery is floating point whilst the cross-pol imagery is complex

For example to create a header file for HHHH data:

    python UAVSARhdr.py \
         -i SMAP13_33010_14112_011_140814_L090_CX_01.ann.txt \
         -r SMAP13_33010_14112_011_140814_L090HHHH_CX_01.grd \
         -p HHHH

Once run, a header file is output into the same directory as the input radar file.

=======================================================================================================

# Original article

Original artcile source: ([here](https://spectraldifferences.wordpress.com/2014/09/29/envi-header-uavsar/))

UAVSAR (Uninhabited Aerial Vehicle Synthetic Aperture Radar) is a high reolution (5m) L-band quad-pol SAR designed, built and operated by the Suborbital Radar and Science Engineering group at the NASA/Caltech Jet Propulsion Laboratory (JPL). Despite being ‘Uninhabited’ by name, UAVSAR is operated by a small team of radar operators aboard a Gulfstream-III twin-engine aircraft. The role of UAVSAR is to collect radar data for a wide range of scientific applications and to provide on-demand imagery over specific regions following natural/environmental disasters, such as earthquakes. More information on UAVSAR can be found at [uavsar.jpl.nasa.gov](uavsar.jpl.nasa.gov).

As UAVSAR is funded by the US government, all UAVSAR data is available to download for free, providing a wealthy source of high quality data for use by those in the field of remote sensing. UAVSAR data has been collected over North and Central America, South America and Greenland and is working towards satisfying flight requests across the globe. UAVSAR data can be downloaded from [uavsar.jpl.nasa.gov/cgi-bin/data.pl](uavsar.jpl.nasa.gov/cgi-bin/data.pl).

Whilst the data is freely available to download, it is provided in grid (.grd) format without accompanying header file, limiting its immediate use within open source and preprioritory software. The data is provided with no means of building a header file, only an accompanying text file of the sensor parameters. Each file therefore, requires that either a header file is hand written or is built in preprioritory software, such as Excelis’ ENVI. Whilst this is achievable with little effort, it can become a laborious task when large quantities of data are required.

To automatically generate header files a Python script (UAVSARhdr.py) has been written. The script parses a parameters text file, which can be downloaded alongside the UAVSAR image, and selects the key parameters from it that are required to build an ENVI formatted header file. These parameters include the number of lines and samples and datatype of the image. Furthermore, the script also projects the image to a geographic lat/long co-ordinate system with the correct pixel spacing (5m). The script is designed to create header files for PolSAR data only.

UAVSAR data is provided in one of two formats. The first is a slant-range product and the second is an orthorectified product. As the slant-range product is often only required by the specialist user, this post focuses on the more commonly used orthorectified product only.

The Python script requires 3 command line option inputs:

**_-i_** – INPUT TXT FILE: The image parameters text file which is parsed by the script

**_-r_** – INPUT RADAR FILE: The input radar UAVSAR image in ‘.grd’ format. The image file is not opened or processed in any way but is used merely to create a header file with a name that matches the radar image

**_-p_** – IMAGE POLARIZATION: The polarization of the scene is required as cross-pol and co-pol imagery will have different data types. The co-pol imagery is floating point whilst the cross-pol imagery is complex

For example to create a header file for HHHH data:

    python UAVSARhdr.py \
         -i SMAP13_33010_14112_011_140814_L090_CX_01.ann.txt \
         -r SMAP13_33010_14112_011_140814_L090HHHH_CX_01.grd \
         -p HHHH

Once run, a header file is output into the same directory as the input radar file.
