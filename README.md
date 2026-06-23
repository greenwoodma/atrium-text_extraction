# ATRIUM PDF Text Extraction

A script for extracting text frm PDF files and storing it into a simple JSON structure which can also store metadata and section (or annotation) information.

## Installation

The script uses a number of Python packages which can be installed from the `requirements.txt` file. We recommend using a virtual enviroment for this to avoid clashes with other projects.

```
python -m venv venv
./venv/bin pip install -r requirements.txt
```

Note that if you wish to run OCR on the PDF before extracting the text then this requires OCRmyPDF to also be installed so that the platform native tools are available. Instructions for how to do this for your platform are available [here](https://ocrmypdf.readthedocs.io/en/latest/installation.html).


## Usage

Once the dependencies are installed you can run the script

```
./venv/bin/python pdf_to_json.py -h
```

which will display this helpful usage message:

```
usage: ATRIUM PDF Text Extraction [-h] --pdf PDF --json JSON [--ocr]

options:
  -h, --help   show this help message and exit
  --pdf PDF    PDF to extract text from
  --json JSON  JSON file to write output into
  --ocr        Run OCR before extracting text
```

As you can see for basic operation simply provide the path to the PDF file using the '--pdf' argument and the path to where to store the JSON output via the `--json` argument. If you also want to perform OCR then simply add the `--ocr` flag.

Note that for PDF files which were [born digital](https://en.wikipedia.org/wiki/Born-digital) it is unlikely you will want to run the OCR step. On PDF files which were created by scanning and OCRing paper documents sometimes it is useful to re-do the OCR as the performance may well have improved since they were originally produced.

## Json Output Format

The output JSON follows the following simple format, where the text is stored as a single top level field, and then section information is provided as offset level information.

```
{
	"meta": {
		(any metadata about the source document)
	},
	"text": (full text contents of the document),
	"sections": [
		{ 
			"start": (number),	<-- character position
			"end": (number),	<-- character position
			"type": (string) 	<-- e.g. "title", "subtitle", "abstract", "conclusions", "references" etc.
		}
	]
	
}
```
