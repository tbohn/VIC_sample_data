# WalnutGulch Sample Dataset

## Files

### Observations

- `obs/WalnutGulch/` - observations from two AMERIFLUX eddy covariance towers within the Walnut Gulch experimental watershed
    - `WHS/` - observations from the Walnut Gulch Lucky Hills Shrub tower
    - `WKG/` - observations from the Walnut Gulch Kendall Grassland tower
    - All site subdirectories contain the following contents, where `$SiteCode` is one of [`WHS`, `WKG`]:
        - `flux_obs/` - original AMERIFLUX observation files at 30-minute resolution; ascii, comma-separated
        - `stdfmt/` - reformatted AMERIFLUX observation files; ascii, space-separated
            - `$prefix.stdfmt.30min.txt` = space-delimited ascii file containing 30-minute resolution observations, where $prefix = the file prefix used in the `flux_obs/` directory; columns:
                - `YYYY MM DD HH MM` = year, month, day, hour, minute  
                - `PREC` = Precipitation (mm)  
                - `Tair` = Air Temperature (C)  
                - `SWdown` = Downward Shortwave (W/m2)  
                - `LWdown` = Downward Longwave (W/m2)  
                - `RH` = Relative Humidity (%)  
                - `Patm` = Atmospheric Pressure (kPa)  
                - `Wind` = Wind Speed (m/s)  
                - `ET` = Evapo-transpiration (mm)  
                - `Tsdep1` = 1st soil observation depth (cm)  
                - `Tsdep2` = 2nd soil observation depth (cm)  
                - `Tsdep3` = 3rd soil observation depth (cm)  
                - `Tsdep4` = 4th soil observation depth (cm)  
                - `Tsdep5` = 5th soil observation depth (cm)  
                - `SM1` = Soil moisture (mm/mm) at Tsdep1  
                - `SM2` = Soil moisture (mm/mm) at Tsdep2  
                - `SM3` = Soil moisture (mm/mm) at Tsdep3  
                - `SM4` = Soil moisture (mm/mm) at Tsdep4  
                - `SM5` = Soil moisture (mm/mm) at Tsdep5  
                - `Tsoil1` = Air Temperature (C) at Tsdep1  
                - `Tsoil2` = Air Temperature (C) at Tsdep2  
                - `Tsoil3` = Air Temperature (C) at Tsdep3  
                - `Tsoil4` = Air Temperature (C) at Tsdep4  
                - `Tsoil5` = Air Temperature (C) at Tsdep5  
                - `SWnet` = Net shortwave (W/m2)  
                - `LWnet` = Net longwave (W/m2)  
                - `H` = Sensible heat flux (W/m2)  
                - `LE` = Latent heat flux (W/m2)  
                - `FG` = Ground heat flux (W/m2)  
              Missing values are denoted by -9999.
            - `$SiteCode.stdfmt.hourly.txt` = space-delimited ascii file containing hourly observations, with the same columns as 30-minute file, but without a minute column
            - `$SiteCode.stdfmt.hourly.local.txt` = same as `$SiteCode.stdfmt.hourly.txt` but with times in local time zone rather than UTC
            - `$SiteCode.stdfmt.daily.txt` = space-delimited ascii file containing daily observations, with the same columns as the hourly files, but without an hour column
        - `vic_force/` = meteorological inputs formatted for VIC; files include:
            - `$SiteCode.vic_force.hourly.txt` = hourly meteorological observations, formatted as inputs to the VIC model; columns:
                - `YYYY MM DD HH` = year, month, day, hour  
                - `Prec` = hourly total precipitation (mm)  
                - `Tair` = hourly air temperature (C)  
                - `SWdown` = hourly downward shortwave (W/m2)  
                - `LWdown` = hourly downward longwave (W/m2)  
                - `Density` = hourly air density (kg/m3)  
                - `Patm` = hourly atmosperic pressure (kPa)  
                - `VP` = hourly vapor pressure (kPa)  
                - `Wind` = hourly wind speed (m/s)  
              Missing values are denoted by -9999.
            - `$SiteCode.vic_force.daily.txt` = daily meteorological observations, formatted as inputs to the MetSim disaggregation algorithm; columns:
                - `YYYY MM DD` = year, month, day  
                - `Prec` = daily total precipitation (mm)  
                - `Tmax` = daily maximum air temperature (C)  
                - `Tmin` = daily minimum air temperature (C)  
                - `Wind` = daily average wind speed (m/s)  
              Missing values are denoted by -9999.
            - `full_data_$lat_$lon` = continuous (gap-filled) hourly meteorological forcings formatted for VIC, where `$lat` and `$lon` are the coordinates of the flux tower; generated by filling gaps in the observed meteorology with gridded forcings from Livneh et al. (2015) via the following steps:
                1. Fill gaps in the daily observed meteorology (`stdfmt/$SiteCode/vic_force/$SiteCode.vic_force.daily.txt`) with values from the Livneh et al. (2015) grid cell (with temperature values lapsed to the flux tower elevation using a lapse rate of 6.5 C / km)  
                2. Disaggregate the merged daily meteorology to hourly via MetSim  
                3. Fill gaps in the hourly observed meteorology (`stdfmt/$SiteCode/vic_force/$SiteCode.vic_force.hourly.txt`) with values from the file generated by step b  
              These files are formatted as inputs to the VIC model; columns:
                - `YYYY MM DD HH` = year, month, day, hour  
                - `Prec` = hourly total precipitation (mm)  
                - `Tair` = hourly air temperature (C)  
                - `SWdown` = hourly downward shortwave (W/m2)  
                - `LWdown` = hourly downward longwave (W/m2)  
                - `Density` = hourly air density (kg/m3)  
                - `Patm` = hourly atmosperic pressure (kPa)  
                - `VP` = hourly vapor pressure (kPa)  
                - `Wind` = hourly wind speed (m/s)  

### Image Driver

- `image/WalnutGulch/parameters/` - parameter files
    - Global Parameter Files:
        - `global_param.WalnutGulch.L2015.txt`
            - Domain File: `domain.WalnutGulch.0.0625_deg.nc`
            - Parameter File: `params.WalnutGulch.L2015.0.0625_deg.nc`
            - Forcings: `livneh_NAmerExt_15Oct2014.WalnutGulch.2008.nc`
        - `global_param.WalnutGulch.MOD_IGBP.txt`
            - Domain File: `domain.WalnutGulch.0.0625_deg.nc`
            - Parameter File: `params.WalnutGulch.MOD_IGBP.0.0625_deg.nc`
            - Forcings: `livneh_NAmerExt_15Oct2014.WalnutGulch.2008.nc`
            - fcanopy is ignored 
        - `global_param.WalnutGulch.MOD_IGBP.Fcanopy.txt`
            - Domain File: `domain.WalnutGulch.0.0625_deg.nc`
            - Parameter File: `params.WalnutGulch.MOD_IGBP.0.0625_deg.nc`
            - Forcings: `livneh_NAmerExt_15Oct2014.WalnutGulch.2008.nc`
            - fcanopy is used 
    - Domain Files:
        - `domain.WalnutGulch.0.0625_deg.nc`
            - 0.0625 degree resolution
            - Taken from Bohn et al. (2018)
    - Parameter Files:
        - `params.WalnutGulch.L2015.0.0625_deg.nc`
            - 0.0625 degree resolution
            - Parameters taken from Livneh et al. (2015)
            - NLDAS soil, snow, and veg parameters
        - `params.WalnutGulch.MOD_IGBP.0.0625_deg.nc`
            - 0.0625 degree resolution
            - MOD-LSP MOD_IGBP parameters (Bohn and Vivoni, 2019)
            - Soils and snowbands from NLDAS
            - Land cover, LAI, fcanopy, and albedo from MODIS

- `image/WalnutGulch/forcings/` - meteorological forcing files
    - `livneh_NAmerExt_15Oct2014.WalnutGulch.2008.nc`
        - 0.0625 degree resolution
        - 3-hour time step
        - 366 days of records
        - From Livneh et al. (2015)
    - NOTE: these are gridded forcings, as opposed to the flux tower forcings in the `obs/WalnutGulch/AMERIFLUX/$SiteCode/vic_force/` directories.

### Classic Driver

Currently there are no classic driver parameters for this dataset. However, classic driver forcings are available in the `obs/WalnutGulch/AMERIFLUX/$SiteCode/vic_force/` directories. Classic driver parameters could be created by appropriate reformatting of the image-driver paramters.

## References
 - Bohn, T. J, and E. R. Vivoni, 2019: MOD-LSP: MODIS-Based Parameters for Variable Infiltration Capacity (VIC) Model over the Continental US, Mexico, and Southern Canada (Version 1.0) [Data set]. Zenodo, doi:10.5281/zenodo.2612560. https://zenodo.org/record/2612560.
 - Bohn, T. J., K. M. Whitney, G. Mascaro, and E. R. Vivoni, 2018: Parameters for PITRI Precipitation Temporal Disaggregation over continental US, Mexico, and southern Canada, 1981-2013 (Version 1.1) [Data set]. Zenodo, doi:10.5281/zenodo.2564019. http://zenodo.org/record/2564019.
 - Livneh, B., T. J. Bohn, D. W. Pierce, F. Munoz-Arriola, B. Nijssen, R. Vose, D. R. Cayan, and L. Brekke, 2015: A spatially comprehensive, hydrometeorological data set for Mexico, the U.S., and southern Canada 1950–2013. Nat. Sci. Data, 2, 150042, doi:10.1038/sdata.2015.42.