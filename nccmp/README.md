# nccmp - NetCDF compare tool

nccmp allows for comparison of two NetCDF files.

## Usage

The easiest way to use this image is to have the two files in the same directory.
Then, binding the current directory to `/data` allows for easy passing of the files with their real names.
Lets `file1.nc` and `file2.nc` be your files:

```shell
docker run --rm -it -v .:/data quepas/nccmp ./file1.nc ./file2.nc -dfqS
```

The `nccmp` common flags are:
* `-d` -> compare data
* `-f` -> don't stop at the first difference
* `-q` -> be quite
* `-S` -> show statistics of differences at the end

## Example output

```shell
Variable Group  Count          Sum      AbsSum          Min         Max       Range         Mean      StdDev
U850     /         20 -4.17286e-07 2.47377e-06 -9.53674e-07 9.53674e-07 1.90735e-06 -2.08643e-08 3.27589e-07
V850     /       3934  3.80972e-07 4.10565e-06 -2.38419e-07 1.19209e-07 3.57628e-07  9.68409e-11 6.58841e-09
W850     /     648000         -nan        -nan    -0.319806    0.260418    0.580224         -nan        -nan
OMEGA850 /     647981      5.94046     159.177    -0.044707    0.045436    0.090143  9.16764e-06  0.00151631
```
