# Data File Formats

## Commonly used data formats in physics

Data files come in many formats. The best file formats embed `metadata` — the information you need to know what the data is! — in the file itself. Large scale experiments — particularly those involving national or international facilities — will almost always use specialized metadata-included file formats. 

The second best file formats provide that metadata in a supplementary "README" file to be included with the data file itself. This is the most common approach at the individual lab level. 

The worst file formats assume the data array names and measurement units are already known. Beginning students often create spreadsheet files lacking information about units, and sometimes national labs that should know better do as well.   **Do not do that.** [The consequences](https://nces.ed.gov/pubs2009/metadata/exhibit1_1.asp) can be dire! 

### spreadsheet data files (.csv)

 on the individual lab level, you are more likely to create files using a spreadsheet, each column of the spreadsheet corresponding to an array of data for a particular measurement (such as current output from a photodiode or voltage measured across a current carrying resistor). The spreadsheet is then exported in `.csv` (comma-separated variables) or `.tbl`(tab delimited) format for import into a data analysis program. 

Opportunities for inclusion of metadata in a spreadsheet are limited. The most common practice is to use the first row — the "header" — of the spreadsheet for to store the name of the data arrays corresponding to each column in the spreadsheet and also, optionally, indicate the units for the measurement. An example would be  `I_photodiode_(mA)` for a measurement of photodiode current in milliamps. 

Alternatively, the first row of the header can be reserved for data array names and a second row added for the measurement units. Although less common, this format brings several advantages, including the ability to add a third row for amplifier gains to indicate when the voltage recored by a computer is not the same as the voltage measured by the measuring instrument. An example would be when a lock-in amplifier uses a gain of 1000 to convert a input voltage of $ 100 \mu V$ into an output voltage of $ 10 V$ and that output voltage is then recorded by a computer. 

Both of these arrangements for spreadsheet headers are compatible with Python data analysis packages such as Numpy,  [Pandas ](https://pandas.pydata.org) and [Polars](https://pola.rs). Examples are provided elsewhere in this handbook. 

The question then becomes as to how to include any additional comments and metadata. One approach is to add several lines of comments at the start of the file once the spreadsheet has been converted into  a `.csv` or `.tbl` text file. This can be accommodated by adding an instruction for Numpy, Pandas, or Polars to skip a certain number of lines in the file. 

A better approach, however, is to create a supplementary readme file that provides a fuller description of each data array and file (if there are multiple files with the same format), then include that file along with the data file(s) and data analysis file that illustrates what the data represents and how it is used.  We will use the text-based markdown (.md) file format for README files, since this is also the format used to include text in Jupyter notebooks and by data and Python respositories (such as FigShare, GitHub,  Zenodo).    


### hierarchical data file systems with embedded metadata 

These take more work to create but are critical for the management of large data sets. Here we mention a few such file formats typically encountered in physics. 

#### HDF

The most commonly encountered  metadata-included file format in physics is  [HDF5](https://www.hdfgroup.org/solutions/hdf5/) (Hierarchical Data Format Version 5), an open-source file format designed to manage, store, and share large, complex, and heterogeneous scientific data. In HDF5, data is organized hierarchically into groups (folders) and datasets (files). User-defined named attributes — the metadata — are attached directly to these groups and datasets so as to make the data self-explanatory. Multiple groups and datasets are included in a single HDF5 file. A similar metadata-included file format in astronomy is [FITS](https://en.wikipedia.org/wiki/FITS) (Flexible Image Transport System) file format. 

#### JSON

In data science, however, you are more likely to come across data in JSON (JavaScript Object Notation) file format, a human and machine readable format based on JavaScript. Some information about the data is provided by the file headers of a JSON document, but you will also usually need files detailing the JASON Schema for the file. This schema defines the expected [(structure, constraints, and data types of the JSON document (called an "instance"). The particle accelerator at [CERN](https://archiver-project.eu/deployment-scenarios-technical-summaries/cern-open-data) uses JSON and a particular JASON Schema for its data and metadata. 

#### Bluesky

[Bluesky](https://blueskyproject.io) is a data format used at DOE Office of Science facilities including Brookhaven National Lab, the National Synchrotron Light Source, Argonne National Lab, SLAC, and Lawrence Berkeley National Lab.  A primary design goal of Bluesky is to enable better research by recording rich metadata alongside measured data for use in later analysis. Documents are how Bluesky does this.

A document is Bluesky's term for a Python dictionary with a schema. The bluesky RunEngine emits documents during plan execution. All of the metadata and data generated by executing the plan is organized into documents. Bluesky’s document-based data model supports complex, asynchronous data collection and enables sophisticated live, prompt, streaming, and post-facto data analysis.

The bluesky documentation describes how outside functions can “subscribe” to a stream of these documents, visualizing, processing, or saving them. [This section](https://blueskyproject.io/event-model/main/explanations/data-model.html) provides an outline of documents themselves, aiming to give a sense of the structure and familiarity with useful components.

