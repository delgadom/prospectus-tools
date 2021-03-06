1. Installation:

On Shackleton, download the Prospectus Tools git repository:
git clone https://github.com/jrising/prospectus-tools/

2. Collect results for each type of file for a given aggregated region:

From within the gcp/extract directory (in that tools repo), run the following
python byrcpssp.py configs/timeseries.yml BASE-FILENAME REGION

BASE-FILENAME is the filename part of files in each of the individual result directories.
REGION is any region specified in those files: global, an ISO3 country, or a FUND region specified in the form FUND-XXX.

So, for example, to generate all of the timeseries needed for the global aggregation, I do:

python byrcpssp.py configs/timeseries.yml interpolated_mortality_all_ages-histclim-aggregated global
python byrcpssp.py configs/timeseries.yml interpolated_mortality_all_ages-aggregated global
python byrcpssp.py configs/timeseries.yml interpolated_mortality_dumb_all_ages-aggregated global
python byrcpssp.py configs/timeseries.yml interpolated_mortality_comatose_all_ages-aggregated global
python byrcpssp.py configs/timeseries.yml interpolated_mortality_all_ages-costs-aggregated global costs_lb
python byrcpssp.py configs/timeseries.yml interpolated_mortality_all_ages-costs-aggregated global costs_ub

3. Generate the various median across kinds of results

The quantilebyrcpssp.py script has slightly different handling for specific kinds of files.  First, the syntax is:

python quantilebyrcpssp.py COLLECTED-FILES-DIRECTORY CLASS-OF-RESULT

Where COLLECTED-FILES-DIRECTORY is the full path to one of the directories generated by the byrcpssp.py script.  CLASS-OF-RESULT can be one of the following:

 - aggfull: full adaptation result (subtracting histclim).
 - aggdumb or aggcoma: just like the full adaptation result, but for dumb or comatose farmers.
 - aggcost1 and aggcost2: lower and upper bounds on the costs.

So, to generate the global costs timeseries data, I do:

python quantilebyrcpssp.py /shares/gcp/outputs/timeseries/rcp85-SSP3-global/ aggfull
python quantilebyrcpssp.py /shares/gcp/outputs/timeseries/rcp85-SSP3-global/ aggdumb
python quantilebyrcpssp.py /shares/gcp/outputs/timeseries/rcp85-SSP3-global/ aggcoma
python quantilebyrcpssp.py /shares/gcp/outputs/timeseries/rcp85-SSP3-global/ aggcost1
python quantilebyrcpssp.py /shares/gcp/outputs/timeseries/rcp85-SSP3-global/ aggcost2