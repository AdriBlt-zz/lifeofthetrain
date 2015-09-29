# Life of the Train

D3 based representation of train's delay and custemers flow within.

### Use
To generate the graph, you can either:
* Directly call the `plotTrains(dataRoute, dataCustemers, "#containerId")` function, with:
  * `dataRoute` the json data of trains timetable and delay (see description below)
  * `dataCustemers` the json data of custemers flow within the trains (see description below)
  * `#containerId` the HTML container ID in which one wants to plot the graph (if undefined or inexistant in the HTML page, the graph will be plot in `body`)

* Call the `plotTrainsFromTSV("dataRoute.tsv", "dataCustemers.tsv", "#containerId")` function that read two TSV (tablation separated values) that contain the data, with:
  * `dataRoute.tsv` the data needed to build `dataRoute` (see columns below)
  * `dataCustemers.tsv` the data needed to build `dataCustemers` (see columns below)
  * `#containerId` the HTML container ID (see above)

* Or call the `plotRandomTrains(nbNums, nbDays, "#containerId")` function that randomly generate data, with:
  * `nbNums` the number of *train number* wanted
  * `nbDays` the number of days for each *train number*
  * `#containerId` the HTML container ID (see above)

### Data Structure

### Data TSV Columns

### Javascript Parameters
