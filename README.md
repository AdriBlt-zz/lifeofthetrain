# Life of the Train

D3 based representation of train's timetable, delay and custemers flow within.

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
To plot a train's timetable, one always needs to specify the `dataRoute` element.
It is basically a list of points that represent the passage of a train at a specific time and space.
The elements of the list contains the following attributes:
  * `number`: [*String*] Number of the train
  * `day`: [*String*] Date of circulation (any format, not parsed)
  * `pointId`: [*String*] ID of the route point
  * `pointName`: [*String*] Name of the route point
  * `hour`: [*Date*] Theoric hour of passage at route point
  * `delay`: [*Integer*] Delay in minutes of the train at the passage (optional)
  * `type`: [*String*] Type of passage ("D"=Departure, "P"=Passage/Transit, "A"=Arrival)

To see the flow of custemers within the train, one shall also provide the `dataCustemers` element.
This is also a list of element describing a flow of custemer within a train.
The elements of the list contains the following attributes:
  * `number`: [*String*] Number of the train
  * `day`: [*String*] Date of circulation (any format, not parsed)
  * `inPoint`: [*String*] ID of the route point where custemers get on the train
  * `outPoint`: [*String*] ID of the route point where custemers get off the train
  * `nbCustemers`: [*Integer*] Number of custemers of the flow
The specified train (`number` + `day`) must be in the `dataRoute` list or the data will be ignored.

### Data TSV Columns
Similarly to the data structure, the TSV files contain the following columns:
  * Route Data:
    * `number`: [*String*] Number of the train
    * `day`: [*String*] Date of circulation (any format, not parsed)
    * `pointId`: [*String*] ID of the route point
    * `pointName`: [*String*] Name of the route point
    * `hour`: [*Date*] Theoric hour of passage at route point **(format "HH:MM:SS", with HH from 0 to 23)**
    * `delay`: [*Integer*] Delay in minutes of the train at the passage (optional)
    * `type`: [*String*] Type of passage ("D"=Departure, "P"=Passage/Transit, "A"=Arrival)
    * `obs`: [*String*] Observations (not used, but may figure in future version. ex: causes of delay)
  
  * Custemers Data
    * `number`: [*String*] Number of the train
    * `day`: [*String*] Date of circulation (any format, not parsed)
    * `inPoint`: [*String*] ID of the route point where custemers get on the train
    * `outPoint`: [*String*] ID of the route point where custemers get off the train
    * `nbCustemers`: [*Integer*] Number of custemers of the flow

**The order of the columns do not import but the columns' names must be the same as the algorithm uses _d3js_ TSV reader (based on columns name).**

### Javascript Parameters
In the begining of the javascript file, there is a small section called "Parameters" where one can find all parameters used for the graphic plot.

 * First of all, there is the `labels` definition.
All legends and texts are listed there and are easily editable.
Labels have been edited in French and English, feel free to complete them with more languages.

* Then come the dimensions of the svg element (`margin`, `width` and `height`) to rescale the global graph.

* One can change the colors used:
  * `selectionColor` represent the mouse over areas color
  * `delayColor` and `custemersDelayColor` are the two colors for train and custemers delay
  * `minCustemersColor` and `maxCustemersColor` represent the extrema values of the custemers area stack color scale

* `deltaTimeOriginTerminus` is the time (in millisec) that is added on the time axis before the origin and after the terminus to better see both of them

* `transformationDuration` is the time (in millisec) of the transformation of the delay line when clicking the delay button (to switch between train's and custemers' delay)

* `custemersInterpolation`, `delayInterpolation` and `stackOffset` are three parameters used in *d3js* interpolation function (all other possible values are listed in the file)

* `radius` and `angle` are used to rotate and offset the timetable points legend

* Finally, `minimumDomainLength` gives a minimum domain length for delay values
