# rUNSWift docs

[![Documentation Status](https://readthedocs.org/projects/runswift/badge/?version=latest)](https://runswift.readthedocs.io/en/latest/?badge=latest)
 

Repository for maintaining the Sphinx Documentation for rUNSWift.

## Installing Dependencies

```
pip3 install -r requirements.txt
```

## Compiling
To compile locally, run `make html`.
The home documentation page can be opened by opening `build/html/index.html` in a browser.

## RTD
The instructions for setting up the webhook for readthedocs is [here](https://docs.readthedocs.io/en/stable/webhooks.html#webhook-creation). For access to the project on readthedocs, [contact us](https://runswift.readthedocs.io/en/latest/contact.html).

## Editing Flowcharts (with draw.io)
`source/draw.io/` contains **.png (with embedded XML)** that can be imported/exported by draw.io.
To modify a diagram,
1. import the png file into draw.io
2. make ammendments
3. overwrite png file by exporting from draw.io
